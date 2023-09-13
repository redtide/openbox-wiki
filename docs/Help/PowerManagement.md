# Power Management

Openbox does not load power management by default - you must load it,
or configure it to load in [autostart](Autostart.md).

There are various options you may have available, depending on your
distribution.

## pm-utils

[pm-utils](https://pm-utils.freedesktop.org/wiki/) gives shell commands such as
`pm-hibernate` and `pm-suspend`.<br />
[pm-utils on the Arch wiki](https://wiki.archlinux.org/index.php/Pm-utils)
has configuration details.

## acpid

[acpid](https://acpid.sourceforge.net/) is a flexible and extensible daemon
for delivering ACPI events, including events triggered by:

- Pressing the power button
- Pressing a sleep/suspend button
- Closing a laptop/notebook lid
- Plugging or unplugging an AC power adapter from a laptop

See also [acpid on the Arch Wiki](https://wiki.archlinux.org/index.php/Acpid).

## gnome-power-manager

If you have GNOME installed on the same installation of Linux that you
are using with Openbox (or if you don't mind installing a few GNOME
dependencies) you can run
[gnome-power-manager](https://gitlab.gnome.org/GNOME/gnome-power-manager) -
simply type or paste at the command prompt:

```bash
gnome-power-manager
```

Gnome power preferences provides a notify area icon, and lets you adjust
the power managment settings used my gnome-power-manager. run:

```bash
gnome-power-preferences
```

## xfce4-power-manager

`xfce4-power-manager` appears to require fewer dependencies than
`gnome-power-manager`.

## Notify area icons

Both the `Gnome` and the `Xfce4` place icons in the notify area -
this will hopefully work in most or all panels, including `tint2` and `LXPanel`.

## See also

[Suspend and hibernate](SuspendAndHibernate.md)
