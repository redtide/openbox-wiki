[Originally written](https://bbs.archlinux.org/viewtopic.php?id=114702)
by Jamie Nguyen (jnguyen on Archlinux BBS). Example configuration file
can be found [here](obdevicemenu.conf).

```bash
#!/bin/bash

#=============================================================================#
#          FILE: obdevicemenu                                                 #
#       VERSION: 1.7.0                                                        #
#                                                                             #
#   DESCRIPTION: obdevicemenu is an Openbox pipe menu that uses udisks to     #
#                easily mount, unmount or eject removable devices. An         #
#                extensive configuration file allows desktop notifications    #
#                about the success or failure of operations, as well as the   #
#                modification of several other options.                       #
#       LICENSE: GPL2                                                         #
#        AUTHOR: Jamie Nguyen                                                 #
#=============================================================================#

# Copyright (C) 2011 Jamie Nguyen
#
# This program is free software; you can redistribute it and/or modify it
# under the terms of the GNU General Public License v2 as published by the
# Free Software Foundation.
#
# This program is distributed in the hope that it will be useful, but WITHOUT
# ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
# FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for
# more details.
#
# You should have received a copy of the GNU General Public License along with
# this program; if not, write to the Free Software Foundation, Inc.,
# 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301, USA


#-------------------------------------#
#           CONFIGURATION             #
#-------------------------------------#
# {{{

unset GREP_OPTIONS

declare filemanager="/usr/bin/Thunar"
declare notify="/usr/bin/notify-send"
declare notify_options="--expire-time=3000"
declare optical_devices="-E ^/dev/sr[0-9]+"
declare removable_devices="-E ^/dev/sd[b-z][0-9]*|^/dev/mmcblk[0-9]+p*[0-9]*"
declare mount_options="--mount-options nosuid,noexec,noatime"

declare -i show_internal=0
declare -i show_notifications=1
declare -i show_optical_device_filename=1
declare -i show_removable_device_filename=1
declare -i fancy_sort=0
declare -i run_post_mount=0
declare -i run_post_unmount=0

declare -a blacklist=( )

declare CONFIGFILE

if [[-n_"${XDG_CONFIG_HOME}"|-n "${XDG_CONFIG_HOME}"]]; then
    CONFIGFILE="${XDG_CONFIG_HOME}/obdevicemenu/config"
else
    CONFIGFILE="${HOME}/.config/obdevicemenu/config"
fi

if [[!_-f_"${CONFIGFILE}"|! -f "${CONFIGFILE}"]]; then
    CONFIGFILE="/etc/obdevicemenu.conf"
fi

if [[-f_"${CONFIGFILE}"|-f "${CONFIGFILE}"]]; then
    . "${CONFIGFILE}"
    if (( $? != 0 )); then
        printf '%s\n' "<openbox_pipe_menu>"
        printf '%s\n' "<separator label=\"obdevicemenu\" />"
        printf '%s\n' "<item label=\"Failed to source configuration file\" />"
        printf '%s\n' "</openbox_pipe_menu>"
        exit 1
    fi
fi

if ! command -v udisks >/dev/null 2>&1; then
    printf '%s\n' "<openbox_pipe_menu>"
    printf '%s\n' "<separator label=\"obdevicemenu\" />"
    printf '%s\n' "<item label=\"Udisks not installed\" />"
    printf '%s\n' "</openbox_pipe_menu>"
    exit 1
fi
# }}}

#-------------------------------------#
#            INTERNAL API             #
#-------------------------------------#
# {{{

notify() {
    if [ -z "${notify_options}" ]; then
        $notify "$*"
    else
        $notify ${notify_options} "$*"
    fi
}

# Functions to retrieve information. These functions simply parse the output
# of udisks --show-info.
info_blank() {
    udisks --show-info ${1} \
        | grep -m 1 -w "^[[:space:|:space:]]*blank:" \
        | awk '{print $2}'
}
info_ejectable() {
    udisks --show-info ${1} \
        | grep -m 1 -w "^[[:space:|:space:]]*ejectable:" \
        | awk '{print $2}'
}
info_has_media() {
    udisks --show-info ${1} \
        | grep -m 1 -w "^[[:space:|:space:]]*has media:" \
        | awk '{print $3}'
}
info_internal() {
    udisks --show-info ${1} \
        | grep -m 1 -w "^[[:space:|:space:]]*system internal:" \
        | awk '{print $3}'
}
info_label() {
    local info_label=
    info_label="$(udisks --show-info ${1} \
        | grep -m 1 -w "^  label:" \
        | awk '{gsub(/_/,"");$1="";print substr($0, index($0,$2))}')"
    [[-n_"${info_label}"|-n "${info_label}"]] && printf '%s\n' "${info_label}"
}
info_media() {
    udisks --show-info ${1} \
    | grep -m 1 -w "^[[:space:|:space:]]*media:" \
    | awk '{gsub(/_/,"");print $2}'
}
info_model() {
    udisks --show-info ${1} \
        | grep -m 1 -w "^[[:space:|:space:]]*model:" \
        | awk '{gsub(/_/,"");$1="";print substr($0, index($0,$2))}'
}
info_mounted() {
    udisks --show-info ${1} \
        | grep -m 1 -w "^[[:space:|:space:]]*is mounted:" \
        | awk '{print $3}'
}
info_mountpath() {
    udisks --show-info ${1} \
        | grep -m 1 -w "^[[:space:|:space:]]*mount paths:" \
        | awk '{$1="";$2="";print substr($0, index($0,$3))}'
}
info_type() {
    udisks --show-info ${1} \
        | grep -m 1 -w "^[[:space:|:space:]]*type:" \
        | awk '{gsub(/_/,"");print $2}'
}
info_vendor() {
    udisks --show-info ${1} \
        | grep -m 1 -w "^[[:space:|:space:]]*vendor:" \
        | awk '{gsub(/_/,"");$1="";print substr($0, index($0,$2))}'
}
# The size of the device/partition is given in bytes, so let's convert that
# to something more readable. Rounding done in bash is not accurate at all
# but we'll mitigate that by only rounding when the numbers get quite large.
convert_size() {
    local -i old_size="${1}"
    local new_size=

    printf '%s\n' "${old_size}" | grep -ow -E ^[1-9]{1}[0-9]*$ >/dev/null 2>&1
    (( $? != 0 )) && return 1

    if (( old_size > 21474836480 )); then
        new_size="$((${old_size}/1073741824)) GB"
    elif (( old_size > 10485760 )); then
        new_size="$((${old_size}/1048576)) MB"
    elif (( old_size > 10240 )); then
        new_size="$((${old_size}/1024)) kB"
    else
        new_size="${old_size} bytes"
    fi

    printf '%s\n' "${new_size}"
}
info_device_size() {
    local info_device_size=
    info_device_size="$(udisks --show-info ${1} \
        | grep -m 1 -w "^[[:space:|:space:]]*size:" \
        | awk '{print $2}')"
    if [[-n_"${info_device_size}"|-n "${info_device_size}"]]; then
        info_device_size="$(convert_size "${info_device_size}")"
        printf '%s\n' "${info_device_size}"
    fi
}
info_partition_size() {
    local info_partition_size=
    info_partition_size="$(udisks --show-info ${1} \
        | grep -m 1 -w "  size:" \
        | awk '{print $2}')"
    if [[-n_"${info_partition_size}"|-n "${info_partition_size}"]]; then
        info_partition_size="$(convert_size "${info_partition_size}")"
        printf '%s\n' "${info_partition_size}"
    fi
}

# Functions to perform udisks commands.

# Eject the device, unmounting with a call to action_unmount if required.
action_eject() {
    local devname="${1}"
    local -i mounted=0
    mounted="$(info_mounted "${devname}")"
    if (( mounted == 1 )); then
        action_unmount "${devname}"
    fi
    mounted="$(info_mounted "${devname}")"
    if (( mounted == 0 )); then
        if (( show_notifications == 1 )); then
            if command -v "${notify}" >/dev/null 2>&1; then
                notify "$(printf '%s\n' "Ejecting ${devname} ...")"
                notify "$(udisks --eject ${devname})"
            fi
        else
            udisks --eject ${devname}
        fi
    fi
}
# Mount the device if it is not already mounted, and run the post_mount hook
# after a successful mount operation if it has been enabled.
action_mount() {
    local devname="${1}"
    if (( show_notifications == 1 )); then
        if command -v "${notify}" >/dev/null 2>&1; then
            notify "$(printf '%s\n' "Mounting ${devname} ...")"
            notify "$(udisks --mount ${devname} ${mount_options})"
        fi
    else
        udisks --mount ${devname} ${mount_options}
    fi

    if (( run_post_mount == 1 )); then
        post_mount ${devname}
    fi
}
# Open the device with the filemanager specified in the configuration file,
# mounting with a call to action_mount if required.
action_open() {
    local devname="${1}"
    local info_mountpath="$(info_mountpath "${devname}")"
    if [[-n_"${info_mountpath}"|-n "${info_mountpath}"]]; then
        $filemanager "${info_mountpath}"
    else
        $filemanager
    fi
}
# Unmount the device if it is not already unmounted, and run the post_unmount
# hook after a successful unmount operation if it has been enabled.
action_unmount() {
    local devname="${1}"
    if (( show_notifications == 1 )); then
        if command -v "${notify}" >/dev/null 2>&1; then
            notify "$(printf '%s\n' "Unmounting ${devname} ...")"
            notify "$(udisks --unmount ${devname})"
        fi
        mounted="$(info_mounted ${devname})"
        if (( mounted == 1 )); then
            notify "$(printf '%s\n' "${devname} unmounted successfully")"
        fi
    else
        udisks --unmount ${devname}
    fi

    if (( run_post_unmount == 1 )); then
        post_unmount ${devname}
    fi
}
action_unmount_all() {
    for devname in $*; do
        action_unmount ${devname}
    done
}
action_info() {
    local devname="${1}"
    local devmajor="${devname%%[0-9]*}"

    udisks --show-info ${devname} >/dev/null 2>&1
    if (( $? != 0 )); then
        printf '%s\n' "<openbox_pipe_menu>"
        printf '%s\n' "<item label=\"Udisks failed.\" />"
        printf '%s\n' "</openbox_pipe_menu>"
        exit 0
    fi

    local info_label="$(info_label "${devname}")"
    local info_vendor="$(info_vendor "${devmajor}")"
    local info_model="$(info_model "${devmajor}")"
    local info_device_size="$(info_device_size "${devmajor}")"
    local info_type="$(info_type "${devname}")"
    local info_media="$(info_media ${devname})"

    if [["${devname}"_!=_"${devmajor}"|"${devname}" != "${devmajor}"]]; then
        local info_partition_size="$(info_partition_size "${devname}")"
    fi

    printf '%s\n' "<openbox_pipe_menu>"

    printf '%s\n' "<separator label=\"Device information\" />"

    [[-n_"${info_device_filename}"|-n "${info_device_filename}"]] && \
        printf '%s\n' "<item label=\"device: ${devname}\" />"
    [[-n_"${info_label}"|-n "${info_label}"]] && \
        printf '%s\n' "<item label=\"label: ${info_label}\" />"
    [[-n_"${info_vendor}"|-n "${info_vendor}"]] && \
        printf '%s\n' "<item label=\"vendor: ${info_vendor}\" />"
    [[-n_"${info_model}"|-n "${info_model}"]] && \
        printf '%s\n' "<item label=\"model: ${info_model}\" />"
    [[-n_"${info_type}"|-n "${info_type}"]] && \
        printf '%s\n' "<item label=\"type: ${info_type}\" />"
    [[-n_"${info_media}"|-n "${info_media}"]] && \
        printf '%s\n' "<item label=\"media: ${info_media}\" />"
    [[-n_"${info_partition_size}"|-n "${info_partition_size}"]] && \
        printf '%s\n' "<item label=\"size (partition): ${info_partition_size}\" />"
    [[-n_"${info_device_size}"|-n "${info_device_size}"]] && \
        printf '%s\n' "<item label=\"size (device): ${info_device_size}\" />"

    printf '%s\n' "</openbox_pipe_menu>"
}
fancy_sort() {
    # This is a very hacky way to sort devices so that /dev/sdc11 wont come
    # before /dev/sdc2, which happens due to a shortcoming of the sort command.

    # We wont tell bash that partition_number is a number, otherwise it
    # breaks when leading zeros are added (interpreted as hex).
    local devname= devmajor= partition_number=
    local -i array_position=0

    # First lets put a leading zero in front of single digits (sdc1 -> sdc01).
    # We are going to ignore /dev/mmcblk*p* devices... too complicated to sort.
    array_position=0
    for devname in ${removable[@]}; do
        if [["${devname}"_=~_^/dev/dm-[0-9]+|"${devname}" =~ ^/dev/dm-[0-9]+]]; then
            devmajor="${devname%%[0-9]*}"
        elif [["${devname}"_=~_^/dev/fd[0-9]+|"${devname}" =~ ^/dev/fd[0-9]+]]; then
            devmajor="${devname%%[0-9]*}"
        elif [["${devname}"_=~_^/dev/sd[a-z][0-9]+|"${devname}" =~ ^/dev/sd[a-z][0-9]+]]; then
            devmajor="${devname%%[0-9]*}"
        else
            array_position=$((++array_position)); continue
        fi

        if [["${devname}"_=_"${devmajor}"|"${devname}" = "${devmajor}"]]; then
            array_position=$((++array_position)); continue
        fi

        partition_number="${devname#${devmajor}}"
        removable[${array_position}]=${devmajor}$(printf '%02d' "${partition_number}")
        array_position=$((++array_position))
    done

    # Now the device array can be sorted properly.
    removable=( $(printf '%s\n' "${removable[@]}" | sort) )

    # Now let's remove those leading zeros that we added.
    array_position=0
    for devname in ${removable[@]}; do
        if [["${devname}"_=~_^/dev/dm-[0-9]+|"${devname}" =~ ^/dev/dm-[0-9]+]]; then
            devmajor="${devname%%[0-9]*}"
        elif [["${devname}"_=~_^/dev/fd[0-9]+|"${devname}" =~ ^/dev/fd[0-9]+]]; then
            devmajor="${devname%%[0-9]*}"
        elif [["${devname}"_=~_^/dev/sd[a-z][0-9]+|"${devname}" =~ ^/dev/sd[a-z][0-9]+]]; then
            devmajor="${devname%%[0-9]*}"
        else
            array_position=$((++array_position)); continue
        fi

        if [["${devname}"_=_"${devmajor}"|"${devname}" = "${devmajor}"]]; then
            array_position=$((++array_position)); continue
        fi

        partition_number="${devname#${devmajor}}"
        removable[${array_position}]=${devmajor}${partition_number#0}
        array_position=$((++array_position))
    done
}

# }}}

#-------------------------------------#
#           MENU FUNCTIONS            #
#-------------------------------------#
# {{{

device_menu() {
    local -a removable=( )
    local -a optical=( )
    local -a mounted_removable=( )
    local -a mounted_optical=( )
    local -i total_removable=0

    printf '%s\n' "<openbox_pipe_menu>"

    udisks --enumerate-device-files >/dev/null 2>&1
    if [[$?_-ne_0|$? -ne 0]]; then
        printf '%s\n' "<item label=\"Udisks failed.\" />"
        printf '%s\n' "</openbox_pipe_menu>"
        exit 0
    fi

    # Here we list devices matched by the "removable_devices" regex specified in
    # the configuration file.

    printf '%s\n' "<separator label=\"Removable media\" />"

    removable=( $(udisks --enumerate-device-files \
        | grep -ow ${removable_devices} | sort) )

    if (( fancy_sort == 1 )); then
        fancy_sort
    fi

    for devname in ${removable[@]}; do
        local devmajor=
        local info_label=
        local -i info_internal=
        local -i mounted=
        local -i partitions=

        # Check here to see if a device such as /dev/sdb has partitions. If there
        # are partitions, such as /dev/sdb1, then hide /dev/sdb from being shown.
        if [["${devname}"_=~_^/dev/mmcblk[0-9]+p*[0-9]*|"${devname}" =~ ^/dev/mmcblk[0-9]+p*[0-9]*]]; then
            devmajor="${devname%%p[0-9]*}"
            if [["${devname}"_=_"${devmajor}"|"${devname}" = "${devmajor}"]]; then
                partitions="$(udisks --enumerate-device-files \
                    | grep -ow -E ^${devname}p[0-9]+ -c)"
                if (( partitions > 0 )); then
                    continue
                fi
            fi
        else
            devmajor="${devname%%[0-9]*}"
            if [["${devname}"_=_"${devmajor}"|"${devname}" = "${devmajor}"]]; then
                partitions="$(udisks --enumerate-device-files \
                    | grep -ow -E ^${devname}[0-9]+ -c)"
                if (( partitions > 0 )); then
                    continue
                fi
            fi
        fi

        info_internal="$(info_internal "${devmajor}")"

        if (( info_internal == 1 )) && (( show_internal == 0 )); then
            continue
        fi

        if (( info_internal == 0 )) || (( show_internal == 1 )); then

            # Hide blacklisted devices.
            for string in ${blacklist[@]}; do
                udisks --show-info "${devname}" | grep -E "${string}" >/dev/null 2>&1
                (( $? == 0 )) && continue 2
            done

            total_removable=$((++total_removable))

            info_label="$(info_label "${devname}")"
            # If no label is present, then use information about the device
            # instead.
            if [[-z_"${info_label}"|-z "${info_label}"]]; then
                info_label="$(info_label "${devmajor}")"
                [[-z_"${info_label}"|-z "${info_label}"]] && info_label="$(info_model "${devmajor}")"
                [[-z_"${info_label}"|-z "${info_label}"]] && info_label="$(info_vendor "${devmajor}")"
                if [[-z_"${info_label}"|-z "${info_label}"]]; then
                    info_label="No label"
                else
                    info_label="No label (${info_label})"
                fi
            fi

            mounted="$(info_mounted "${devname}")"
            if (( mounted == 0 )); then
                if (( show_removable_device_filename == 1 )); then
                    printf '%s' "<menu id=\"mount${devname}\" "
                    printf '%s' "label=\"${devname#/dev/}: ${info_label}\" "
                    printf '%s' "execute=\"$0 --mount-menu removable "
                    printf '%s' "${devname}\" />"
                    printf '\n'
                else
                    printf '%s' "<menu id=\"mount${devname}\" "
                    printf '%s' "label=\"${info_label}\" "
                    printf '%s' "execute=\"$0 --mount-menu removable "
                    printf '%s' "${devname}\" />"
                    printf '\n'
                fi
            else
                if (( show_removable_device_filename == 1 )); then
                    printf '%s' "<menu id=\"mount${devname}\" "
                    printf '%s' "label=\"${devname#/dev/}: "
                    printf '%s' "${info_label} (mounted)\" "
                    printf '%s' "execute=\"$0 --mount-menu removable "
                    printf '%s' "${devname}\" />"
                    printf '\n'
                else
                    printf '%s' "<menu id=\"mount${devname}\" "
                    printf '%s' "label=\"${info_label} (mounted)\" "
                    printf '%s' "execute=\"$0 --mount-menu removable "
                    printf '%s' "${devname}\" />"
                    printf '\n'
                fi
                mounted_removable[${#mounted_removable[*]}]=${devname}
            fi
        fi
    done

    if (( total_removable == 0 )); then
        printf '%s\n' "<item label=\"None\" />"
    elif (( ${#mounted_removable[*]} > 0 )); then
        printf '%s\n' "<item label=\"Unmount all\">"
        printf '%s\n' "<action name=\"Execute\">"
        printf '%s\n' "<command>$0 --unmount-all-removable \
            ${mounted_removable[*]}</command>"
        printf '%s\n' "<prompt>Unmount all removable devices?</prompt>"
        printf '%s\n' "</action>"
        printf '%s\n' "</item>"
    fi

    # Here we list devices matched by the "optical_devices" regex specified in
    # the configuration file.
    printf '%s\n' "<separator label=\"Optical media\" />"

    optical=( $(udisks --enumerate-device-files \
        | grep -ow ${optical_devices} | sort) )

    if (( ${#optical[*]} == 0 )); then
        printf '%s\n' "<item label=\"None\" />"
        printf '%s\n' "</openbox_pipe_menu>"
        return 0
    fi

    for devname in ${optical[@]}; do
        local info_label=
        local -i info_blank=0
        local -i info_has_media=0
        local -i mounted=0

        info_has_media="$(info_has_media "${devname}")"

        # Hide blacklisted devices.
        for string in ${blacklist[@]}; do
            udisks --show-info "${devname}" | grep -E "${string}" >/dev/null 2>&1
            (( $? == 0 )) && continue 2
        done

        if (( info_has_media == 0 )); then
            printf '%s\n' "<item label=\"${devname#/dev/}: None\" />"
        else
            info_blank="$(info_blank "${devname}")"
            if (( info_blank == 1 )); then
                info_label="Blank media"
            else
                info_label="$(info_label ${devname})"
                [[-z_"${info_label}"|-z "${info_label}"]] && info_label="$(info_model "${devname}")"
                [[-z_"${info_label}"|-z "${info_label}"]] && info_label="No label"
            fi

            mounted="$(info_mounted "${devname}")"
            if (( mounted == 0 )); then
                if (( show_optical_device_filename == 1 )); then
                    printf '%s' "<menu id=\"mount${devname}\" "
                    printf '%s' "label=\"${devname#/dev/}: ${info_label}\" "
                    printf '%s' "execute=\"$0 --mount-menu optical "
                    printf '%s' "${devname}\" />"
                    printf '\n'
                else
                    printf '%s' "<menu id=\"mount${devname}\" "
                    printf '%s' "label=\"${info_label}\" "
                    printf '%s' "execute=\"$0 --mount-menu optical "
                    printf '%s' "${devname}\" />"
                    printf '\n'
                fi
            else
                if (( show_optical_device_filename == 1 )); then
                    printf '%s' "<menu id=\"mount${devname}\" "
                    printf '%s' "label=\"${devname#/dev/}: "
                    printf '%s' "${info_label} (mounted)\" "
                    printf '%s' "execute=\"$0 --mount-menu optical "
                    printf '%s' "${devname}\" />"
                    printf '\n'
                else
                    printf '%s' "<menu id=\"mount${devname}\" "
                    printf '%s' "label=\"${info_label} (mounted)\" "
                    printf '%s' "execute=\"$0 --mount-menu optical "
                    printf '%s' "${devname}\" />"
                    printf '\n'
                fi
                mounted_optical[${#mounted_optical[*]}]=${devname}
            fi
        fi
    done

    if (( ${#mounted_optical[*]} > 0 )); then
        printf '%s\n' "<item label=\"Unmount all\">"
        printf '%s\n' "<action name=\"Execute\">"
        printf '%s\n' "<command>$0 --unmount-all-optical \
            ${mounted_optical[*]}</command>"
        printf '%s\n' "<prompt>Unmount all optical devices?</prompt>"
        printf '%s\n' "</action>"
        printf '%s\n' "</item>"
    fi

    printf '%s\n' "</openbox_pipe_menu>"
}
# Here we provide a submenu for each device, which displays the available
# actions that can be performed.
mount_menu() {
    local media_type="${1}"
    local devname="${2}"
    local info_label="${3}"
    local devname_short="${devname##*/}"
    local -i info_ejectable=0
    local -i mounted=0

    printf '%s\n' "<openbox_pipe_menu>"

    if [["${media_type}"_=_"removable"|"${media_type}" = "removable"]]; then
        if (( show_removable_device_filename == 1 )); then
            printf '%s\n' "<separator label=\"${devname}\" />"
        else
            printf '%s\n' "<separator label=\"${info_label}\" />"
        fi
    elif [["${media_type}"_=_"optical"|"${media_type}" = "optical"]]; then
        if (( show_optical_device_filename == 1 )); then
            printf '%s\n' "<separator label=\"${devname}\" />"
        else
            printf '%s\n' "<separator label=\"${info_label}\" />"
        fi
    fi

    mounted="$(info_mounted "${devname}")"

    if (( mounted == 0 )); then
        printf '%s\n' "<item label=\"Open\">"
        printf '%s\n' "<action name=\"Execute\">"
        printf '%s\n' "<command>$0 --mount-and-open ${devname}</command>"
        printf '%s\n' "</action>"
        printf '%s\n' "</item>"

        printf '%s\n' "<item label=\"Mount\">"
        printf '%s\n' "<action name=\"Execute\">"
        printf '%s\n' "<command>$0 --mount-device ${devname}</command>"
        printf '%s\n' "</action>"
        printf '%s\n' "</item>"
    else
        printf '%s\n' "<item label=\"Open\">"
        printf '%s\n' "<action name=\"Execute\">"
        printf '%s\n' "<command>$0 --open-directory ${devname}</command>"
        printf '%s\n' "</action>"
        printf '%s\n' "</item>"

        printf '%s\n' "<item label=\"Unmount\">"
        printf '%s\n' "<action name=\"Execute\">"
        printf '%s\n' "<command>$0 --unmount-device ${devname}</command>"
        printf '%s\n' "</action>"
        printf '%s\n' "</item>"
    fi

    info_ejectable="$(info_ejectable "${devname}")"

    if (( info_ejectable == 1 )); then
        printf '%s\n' "<item label=\"Eject\">"
        printf '%s\n' "<action name=\"Execute\">"
        printf '%s\n' "<command>$0 --eject-device ${devname}</command>"
        printf '%s\n' "</action>"
        printf '%s\n' "</item>"
    fi

    printf '%s' "<menu id=\"showinfo${devname##*/}\" "
    printf '%s' "label=\"Info\" "
    printf '%s' "execute=\"$0 --show-info ${devname}\" />"
    printf '\n'

    printf '%s\n' "</openbox_pipe_menu>"
}
# }}}

#-------------------------------------#
#              INT MAIN               #
#-------------------------------------#

if (( $# == 0 )); then
    device_menu
    exit 0
fi

# The script calls itself with different options in order to get nested pipe
# menus.
case "${1}" in
    "--mount-menu")
        mount_menu ${2} ${3}
        ;;
    "--mount-device")
        action_mount "${2}"
        ;;
    "--unmount-device")
        action_unmount "${2}"
        ;;
    "--eject-device")
        action_eject "${2}"
        ;;
    "--open-directory")
        action_open "${2}"
        ;;
    "--mount-and-open")
        action_mount "${2}" && action_open "${2}"
        ;;
    "--show-info")
        action_info "${2}"
        ;;
    "--unmount-all-removable")
        shift 1 && action_unmount_all $@
        ;;
    "--unmount-all-optical")
        shift 1 && action_unmount_all $@
        ;;
esac

# vim: set ts=4 sw=4 noet foldmethod=marker :
```
