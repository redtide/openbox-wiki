# FAQ

## How do I set my desktop background?

The example in the [autostart guide](Help/Autostart.md)
sets the background to a solid color.

You can use any number of programs to set your background.
A few commonly used programs are
[xsetroot](https://www.xfree86.org/current/xsetroot.1.html),
[esetroot](https://www.jnrowe.ukfsn.org/projects/esetroot.html),
[hsetroot](#how-do-i-set-my-desktop-background "https://thegraveyard.org/hsetroot.php: 'Nothing here but ashes and dust...'")
and
[nitrogen](https://github.com/l3ib/nitrogen/).
They each have their own set of features. You can use any of these programs
in your autostart to set your wallpaper when you log in.

There are also [pipe menus](Community/Pipemenus/index.md#personalisation)
designed for choosing and setting your wallpaper.

## How do I put my desktops into a grid layout instead of a single row?

Your pager is responsible for doing this, and communicates with Openbox
to make sure they agree on it. Any pager which complies with the EWMH
specification should be able to do this. Examples are the `gnome-panel`
pager and `rox-pager`.

If your pager does not comply with the spec, or you don't use a pager,
you can use [this small program](dist/tools/setlayout.c) to set the layout
at startup, for example setlayout 0 2 2 0 for a 2x2 grid.

## What is this dock I hear so much about?

The dock is where your dockapps go, if you don't have any, you don't
need it. There are some dockapps available in linux distributions such
as
[wiki.archlinux.org/index.php/Window_Maker](https://wiki.archlinux.org/index.php/Window_Maker#Dockapps)
for Arch. Or via thid parties such as
[www.cs.mun.ca/~gstarkes/wmaker/dockapps/other.html](https://www.cs.mun.ca/~gstarkes/wmaker/dockapps/other.html).

## Does anyone know of a taskbar that works well with openbox?

There are many taskbar/panels around. Some examples are: `fbpanel`,
`pypanel`, `perlpanel`, `xfce4-panel` (from XFCE), `gnome-panel` (from GNOME)
and `kicker` (from KDE).

There are many programs [listed here](Help/Session.md)
that you can use with Openbox, including taskbars and other things.

## How do I make things start when I start Openbox?

If you are using a desktop environment - and therefore a session
manager - you just need to save your session with the programs running.
GNOME and KDE's session managers also both provide a way to run things
on startup that aren't a part of the session, see their documentation
for details.

If you run Openbox without a desktop environment and session manager,
see the [autostart guide](Help/Autostart.md).

## How do I run SCIM when I start Openbox?

See the [autostart documentation](Help/Autostart.md) for details
on how to do this and an example that launches SCIM.

## How do I make my dockapps appear in order when I start Openbox?

You can use this in your [autostart file](Help/Autostart.md) to
launch your dockapps and have them show up in the same order every time:

```bash
DELAY=.75
APPS='/home/mwilson/bin/clock \
      /home/mwilson/bin/weather \
      /home/mwilson/bin/grabimage \
      /home/mwilson/bin/awmcpuload \
      /home/mwilson/bin/temp \
      /home/mwilson/bin/net \
      /home/mwilson/bin/i-net0 \
      /home/mwilson/bin/i-net1 \
      wmsysmon \
      wmix'
(for X in $APPS ; do ($X &) ; sleep $DELAY ; done) &
```

Replace each of the commands in `APPS` with the dockapps you want to
run, and they will appear in the dock in the order they are listed. Take
care of having a `\` at the end of each line, except for the last line.

## I'm using rxvt-unicode or aterm, and transparency is leaving artifacts!

This will work in Openbox 3.4. If you are running an older version or
have this problem with another wm, here's what to do: By default these
terminals use a transparency mode that only works by chance. They
support a more proper one too. If you use `aterm` you have to give `-sh 99`
or `-sh 101`, with `urxvt` you have to give `-tint white`
(ie in `urxvt` you can use `-sh 100` and the proper mode).
If this doesn't use the correct background image you have to use
a background setting program that sets the correct hint,
for example `Hsetroot` and `Esetroot`.

## How do I get true 32-bit transparent windows?

True 32-bit transparency is made possible through the Composite extension.
You need to have this extension enabled in your Xserver.
Use this command in a terminal to make sure it is enabled:

```bash
xdpyinfo|grep Composite
```

It will list `Composite` if it is enabled.

As well, you need to run a composite manager for applications to access
the `Composite` extension. You can use the `xcompmgr` with a command like this:

```bash
xcompmgr -c -t-5 -l-5 -r4.2 -o.55 &
```

Run it without any arguments if you don't want any extras like drop shadows.

You could put this command in your
[autostart file](Help/Autostart.md) to make it run automatically at log in.

Lastly, you need an application which supports it, such as `rxvt-unicode`:

```bash
urxvt -depth 32 -fg white -bg rgba:0000/0000/0000/bbbb
```

You can use the `transset` program to give transparency to any window,
with a command such as this:

```bash
transset 0.8  # then click on the window you want to make transparent
```

## How do I remove the decorations from all my windows?

You can use the per-app settings to remove decorations from all your windows,
or any group of them. The per-app settings are in the `<applications>` section
of your `~/.config/openbox/rc.xml` (or the system-wide `/etc/xdg/openbox/rc.xml`).

Here is an example that would remove decorations from all of your windows
except Firefox:

```xml
<applications>
  <!-- match all windows, and remove their decorations -->
  <application class="*">
    <decor>no</decor>
  </application>

  <!-- but give decorations back to Firefox -->
  <application name="Firefox*">
    <decor>yes</decor>
  </application>
</applications>
```

There is a more complicated example showing many of the things you can
do with per-app settings in the
[upgrading to 3.4 guide](Help/UpgradingTo3.4.md#settings-for-specific-windows-per-application-settings).

## Where did my Debian menu go?

The short answer is: nowhere.
If you previously had an official Debian Openbox .deb installed
and saw the Debian Menu in the root menu, the files are all still present
on your system. Openbox.org .debs and/or source installs don't include them
in your root menu -- that's done by Debian developer magic.
You can do it with a few simple steps in
[these instructions](Help/Menus.md#the-debian-menu).

## How do I disable the popup when switching desktops?

Please see the
[upgrading to 3.4 guide](Help/UpgradingTo3.4.md#desktop-cycling-dialog).

## How do I run Openbox across multiple X screens?

In order to have Openbox manage multiple X screens (this is not the same
as multi-monitor TwinView or Xinerama), you need to run an instance of
Openbox directly on each screen. We've put work into making Openbox work
well with other instances of itself, for this type of configuration.

In order to run Openbox on two screens, use commands such as these:

```bash
# run openbox on the second screen (they start from 0)
DISPLAY=:0.1 openbox &
# by default openbox will run on the first screen (screen number 0)
exec openbox-session
```

## How do I make Tweetdeck/Other Adobe Air apps work under Openbox?

Just put:

```bash
export GNOME_DESKTOP_SESSION_ID="openbox"
```

in your `autostart.sh` or `.xinitrc` (the "openbox" part can be any word).
You can then run tweetdeck/twhirl etc. without any problems,
although you might needs some gnome keyring elements installed.
