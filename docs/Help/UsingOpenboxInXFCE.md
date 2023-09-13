# Openbox

## Using Openbox in XFCE 4

<div style="color:#d29922">
Note: You must have Openbox (and possibly ObConf) already installed to use this guide.
</div>

To use Openbox with XFCE, log into your normal XFCE session. Then, run
this command in a terminal:

```bash
openbox --replace & exit
```

This command terminates the currently running window manager, runs Openbox,
and closes the terminal. Now you must log out and log back in.
When you go to log out, make sure you check the box that says
"Save session for future login" or something like that.
When you log back in, XFCE will use Openbox.

Note, if you don't use Xfwm4, this command could fail, depending on the abilities
of the window manager. For example, Fluxbox doesn't accept to be replaced this way.
In this case, you have to run the following
command:

```bash
killall fluxbox ; openbox & exit
```

To be able to exit the session using xfce4-session, open your file
`~/.config/openbox/menu.xml` (if it isn't there, copy it from
`/etc/xdg/openbox/menu.xml`). Look for the entry

```xml
<item label="Exit">
  <action name="Exit"/>
</item>
```

and change it for the following

```xml
<item label="Exit">
  <action name="Execute">
    <command>xfce4-session-logout</command>
  </action>
</item>
```

Otherwise, using the `Exit` entry of the root-menu will cause Openbox
to terminate its execution.

Also, if you notice scrolling the wheel to change between virtual desktops
skips one or another virtual desktop (and this bothers you and
would like to fix it just for mental sake), open your
`~/.config/openbox/rc.xml` file and move the mouse binds with actions
`DesktopPrevious` and `DesktopNext` from the context `Desktop` to the
context `Root` (you may need to define the `Root` context).

If you want to use the Openbox root-menu instead of Xfce's,
(right click over the desktop) you could terminate Xfdesktop
by running the following command in a terminal:

```bash
xfdesktop --quit
```

The bad news is that Xfdesktop manages the wallpaper and desktop icons,
so you should use other tools for that purpose (check the FAQ for some ideas).
By terminating Xfdesktop, the former issue with the virtual desktops
is no longer a problem.
