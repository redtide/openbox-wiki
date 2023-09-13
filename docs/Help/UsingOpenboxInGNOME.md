# Starting Openbox with GNOME

![LoginOptions.png][1] The instructions below don't work with current versions
of GNOME and Openbox versions before 3.4.8. As a workaround,
you can run the command `openbox --replace`
after logging into a standard GNOME session, and cross your fingers.

To log into the GNOME desktop environment with Openbox as your window
manager, select the `GNOME/Openbox` option when logging in through GDM,
which you can see in Figure [1].

If you don't use a graphical log in, you can use the
`openbox-gnome-session` command to start a GNOME session with Openbox as
your window manager.

See the [getting started guide][5] for more details.

## Accessing gnome-panel with key bindings

![GnomeMenuInOpenbox.png][2] If you are using gnome-panel in Openbox
and want to access it with key bindings, you can use the `gnome-panel-control`
program (which is a part of Openbox) to do so.

Here is an example of two bindings to pop up the gnome-panel's main
menu, and to pop up the "Run" dialog:

```xml
<keybind key="A-F1">
  <action name="execute">
    <execute>gnome-panel-control --main-menu</execute>
  </action>
</keybind>
<keybind key="A-F2">
  <action name="execute">
    <execute>gnome-panel-control --run-dialog</execute>
  </action>
</keybind>
```

Just add that to the `<keyboard>` section of your `rc.xml` [configuration file][4],
and change the keys to match your preferences.
The keys shown are the defaults used by Metacity, the default window manager for GNOME.

## Logging out

![GNOMELogout.png][3] In order to log out of GNOME without going through
the `gnome-panel`, you can use the command `gnome-session-save --kill --gui`.

Here is an example of a "Log out" option for a menu:

```xml
<menu id="root-menu">
  ...
  <item label="Log out">
    <action name="Execute"><execute>gnome-session-save --kill --gui</execute></action>
  </item>
</menu>
```

You can also use the same command in a key binding to log out by
pressing a key combination.

The session state may not be preserved when you log out with Openbox
running. You can fix this by restarting Metacity first, for example with
the following shell script.

```bash
  killall openbox
  coproc metacity
  gnome-session-save --logout-dialog
```

And to shut down

```bash
killall openbox
coproc metacity
gnome-session-save --shutdown-dialog
```

## Nautilus and Openbox

If you don't want Nautilus to draw icons on your desktop, you can
disable it with the `gconf-editor` program. Run `gconf-editor` and
browse to `/apps/nautilus/preferences` and turn off the **show desktop**
option. Another simpler way to get that is to call nautilus
with the `--no-desktop switch`.

If you do want icons from Nautilus on your desktop, you should disable
the menu Openbox shows when you right-click on the desktop.
Other desktop programs don't have this problem, but with Nautilus you won't be
able to access its right-click menu unless you disable Openbox's (or use
Shift-Right Click to access the Nautilus menu).
In the default configuration `rc.xml` file, remove the following section
(in the `Root mouse-binding` context):

```xml
<mousebind button="Right" action="Press">
  <action name="ShowMenu"><menu>root-menu</menu></action>
</mousebind>
```

Also, file a bug report for Nautilus so you won't have to do this in the future.


[1]: ../assets/img/LoginOptions.png "Login options"
[2]: ../assets/img/GnomeMenuInOpenbox.png "Gnome menu in Openbox"
[3]: ../assets/img/GNOMELogout.png "GNOME logout"
[4]: Configuration.md
[5]: GettingStarted.md
