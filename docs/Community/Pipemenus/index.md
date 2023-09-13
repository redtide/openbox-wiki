# Pipe menus

![Ob-chromium-scrot]
Pipe menus are generated at run time (on-the-fly) based on output of scripts.
These are also called "dynamic menus," and are often used to provide added
functionality to Openbox or integration with other software on the
system. A number of scripts for generating pipe menus have been
collected on this page. Please note many of these scripts have not been
reviewed, and were not written by people directly involved with the project.

See the [menu documentation] for how to use pipe menus in your Openbox installation.

[Ob-chromium-scrot]:  ../../assets/img/Ob-chromium-scrot.png "ob-chromium"
[menu documentation]: ../../Help/Menus.md#pipe-menus

## Application Menus

| **Script**                     | **Implementation** | **Description**
| ---                            | ---                | ---
| **[openbox-xdgmenu]**          | C                  | Create an XDG menu
| **Openbox [Application Menu]** | Perl               | Reads .desktop files from multiple directories to construct a flat menu. Useful if your system doesn't have working XDG or Debian menus.
| **[obamenu]**                  | Python             | Automagically creates Openbox application menus by analyzing xdg information provided by desktop files.

[openbox-xdgmenu]:  https://launchpad.net/openbox-xdgmenu/+download
[Application Menu]: obam.md
[obamenu]:          https://rmoe.anukis.de/obamenu.html

## Desktop Environment Integration

| **Script**                | **Implementation** | **Description**
| ---                       | ---                | ---
| **[gtk-bookmarks]**       | Bash               | Simple bash script to create a pipe menu from `~/.gtk-bookmarks` by Mulberry
| **[thunar-bookmarks]**    | Perl               | A pipe menu that duplicates `~/.gtk-bookmarks` (Nautilus, PCManFM, Thunar), by [dbbolton]
| **[dolphin-bookmarks]**   | Perl               | A pipe menu that duplicates user-places.xbel (Dolphin, etc) by [dbbolton]
| **[recentfilesxbel]**     | UNIX sh            | Shows your recent documents using the newer xbel format. by [davidbarr]
| **[rox-filer bookmarks]** | Python             | Pipes the rox-filer bookmarks from `~/.config/rox/bookmarks.xml` into the Openbox menu. Running one opens the bookmark in rox-filer.

[gtk-bookmarks]:       gtk-bookmarks.md
[thunar-bookmarks]:    https://github.com/dbbolton/pipemenus/blob/master/thunar-bookmarks.pl
[dolphin-bookmarks]:   https://github.com/dbbolton/pipemenus/blob/master/dolphin-bookmarks.pl
[recentfilesxbel]:     recentfilesxbel.md
[rox-filer bookmarks]: https://icculus.org/openbox/pipemenus/bookmarks.py
[dbbolton]:            ../../User/Dbbolton.md
[davidbarr]:           #desktop-environment-integration "Missing user page"

### Personalisation

| **Script**                | **Implementation** | **Description**
| ---                       | ---                | ---
| **[ob3_theme]**           | C                  | Openbox 3 theme changer by Mike Hokenson
| **[ob3_wall]**            | C                  | Openbox 3 desktop wallpaper changer by Mike Hokenson
| **[show_ob_keybindings]** | Python             | View/edit keybindings by Joe Bloggs
| **[bmenu-1.0]**           | Python             | A pipe menu which uses Feh to select the wallpaper from the chosen directory by Mulberry

[ob3_theme]:           https://www.gozer.org/my_stuff/c/c/ob3_theme.c
[ob3_wall]:            https://www.gozer.org/programs/c/c/ob3_wall.c
[show_ob_keybindings]: https://github.com/vapniks/ob-pipe-menus
[bmenu-1.0]:           bmenu-1.0.md

## Media & Games

| **Script**                            | **Implementation** | **Description**
| ---                                   | ---                | ---
| **[xmms2-OpenboxMenu]**               | Python             | xmms2 Pipe menu client
| **[Audacious Control]**               | Bash               | Controls Audacious from a pipe menu by Matsuda Shinpei
| **[Audacious Control (alternative)]** | Perl               | A menu to control Audacious. Uses a builtin client for Audacious and depends on wmctrl. By [AaylaSecura]
| **[MPD/MPC Control]**                 | Perl               | Control MPD/MPC from a pipe menu. Depends on MPC and one of gtkdialog/matedialog/zenity. By [AaylaSecura]
| **[my_q3stat]**                       | C                  | A script to query Quake 3 servers by Mike Hokenson

[xmms2-OpenboxMenu]:               https://github.com/Eli2/xmms2-OpenboxMenu
[Audacious Control]:               AudaciousControl.md
[Audacious Control (alternative)]: AudaciousControlAlternative.md
[MPD/MPC Control]:                 MPDControl.md
[my_q3stat]:                       https://www.gozer.org/programs/c/files/my_q3stat.c
[AaylaSecura]:                     #media-games "Missing user page"

## System Integration

| **Script**           | **Implementation** | **Description**
| ---                  | ---                | ---
| **[ob-cpufreq] 0.2** | Python             | See your CPU frequency by John McKnight
| **[ob-sysinfo]**     | Perl               | A similar system information script written in Perl and easy to modify/extend by [dbbolton]
| **[date-menu]**      | UNIX sh            | A simple date, time, and calendar.
| **[Reboot Menu]**    | Perl               | Allows you to reboot to the any of the options in your grub.conf.
| **[battery]**        | Bash               | A simple script to show acpi settings battery and temperature.
| **[processes]**      | Python             | Reads out info from /proc and pipes it to a menu. Renice, kill or restart apps through the menu. Has a filter, so not all apps/daemons are shown in the menu. By Vlad George.
| **[ob-randr]**       | Python             | Easily change resolution, rotation, scaling, panning, and other xrandr operations as well as quickly see the capabilities of connected displays.

[ob-cpufreq]:  https://icculus.org/openbox/pipe/ob-cpufreq-0.2.py
[ob-sysinfo]:  https://github.com/dbbolton/pipemenus/raw/master/ob-sysinfo.pl
[date-menu]:   DateMenu.md
[Reboot Menu]: obreboot.md
[battery]:     battery.md
[processes]:   processes-python.md
[ob-randr]:    https://github.com/whiteinge/ob-randr/

### Devices & Files

| **Script**            | **Implementation** | **Description**
| ---                   | ---                | ---
| **[mntmenu]**         | Perl               | Pipe menu that parses /etc/fstab for user mountable filesystems and allows the user to mount them. By Matthew Fitzgibbons.
| **[obdevicemenu]**    | Bash               | Uses udisks to easily mount, unmount or eject removable devices. Extensive configuration allows notifications about success or failure of operation, & modification of several other options. By Jamie Nguyen.
| **[Directory Menu]**  | Perl               | Pipe menu for recursive directory listings.
| **[obfilebrowser]**   | Python             | Display files and directories and generates submenus with commands to open files with their associated applications. By Xyne

[mntmenu]:        mntmenu.md
[obdevicemenu]:   obdevicemenu/index.md
[Directory Menu]: Dirsmenu.md
[obfilebrowser]:  https://xyne.archlinux.ca/projects/obfilebrowser/

## Miscellaneous

### Internet

| **Script**               | **Implementation** | **Description**
| ---                      | ---                | ---
| **[Chromium bookmarks]** | Perl               | Create a pipemenu of chromium/google-chrome bookmarks by [Spoiledbroth]
| **[Firefox bookmarks]**  | Python             | Create a pipemenu of Firefox bookmarks by Manuel Colmenero.
| **[feeder]**             | Python             | A script to pipe RSS and Podcast feeds into the Openbox menu by Vlad George
| **[Weather Pipe Menu]**  | Python             | Shows the weather forecast of the city passed as argument.

[Chromium bookmarks]: ../../User/Spoiledbroth/ob-chromium.md
[Firefox bookmarks]:  obm-mozilla.md
[feeder]:             feeder-python.md
[Weather Pipe Menu]:  https://bbs.archlinux.org/viewtopic.php?id=43432
[Spoiledbroth]:       ../../User/Spoiledbroth/index.md

### Utilities

| **Script**                                  | **Implementation** | **Description**
| ---                                         | ---                | ---
| **[clipboard_menu]**                        | Python             | Menu of recently copied text clips, selecting an item pastes it (requires parcellite or clipit) by Joe Bloggs
| **Palobo's Openbox [SimpleTasks] Tasklist** | Python             | A simple task list in the form of a pipe menu. Simple features are supported for the time being. Adding tasks. Clicking on a task renders it completed and is therefore removed from the list.

[clipboard_menu]: https://github.com/vapniks/ob-pipe-menus/tree/master/clipboard_manager
[SimpleTasks]:    https://bitbucket.org/palobo/simpletasks/

## Script collections

- User/[Baavgai](../../User/Baavgai.md)
- User/[Spoiledbroth]

### External links

- [ArchWiki Openbox Pipes][1]
- [Arch Linux Forums pipe menus][2]
- [zhar.net Openbox stuff][3]
- [Mulberry's Openbox Pipe menu scripts][4]
- [Manuel Colmenero's Openbox Menu Editor][5]
- [BunsenLabs Pipe menus repository][6]
- [Antonio Malcolm's Corgi Scripts repository][7]
- [yeuxdelibad.net Openbox repo][8]
- [Nathan F's obpipes][9]

[1]: https://wiki.archlinux.org/index.php/Openbox#Pipes
[2]: https://bbs.archlinux.org/search.php?action=search&keywords=openbox+pipe+menu&author=&forums=27&search_in=0&sort_by=0&sort_dir=DESC&show_as=topics
[3]: https://zhar.net/projects/openbox/
[4]: https://web.archive.org/web/20150215210422/http://david.chalkskeletons.com/scripts/
[5]: https://obmenu.sourceforge.net/
[6]: https://github.com/BunsenLabs/bunsen-pipemenus/
[7]: https://github.com/antonio-malcolm/corgi-scripts/
[8]: #external-links
"404: https://dev.yeuxdelibad.net/coolrepo/Scripts/Openbox/"
[9]: https://www.murga-linux.com/puppy/viewtopic.php?t=87588
