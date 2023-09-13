# Upgrading to 3.4

Openbox 3.4 looks a lot like previous versions, but once you start using
it, you will see that it is not. There are a huge number of improvements
and changes made in our 3.4 release. This guide goes through all these
changes and what they mean for users, themers, and developers.

<img src="../../assets/img/Cowsay.png" alt="Cowsay.png" width="640px" />

## The "I don't have time give me something fast" approach

There are a number of new things that you won't be able to take
advantage of without updating your configuration file. One quick and
easy way to get these features is to just delete your
`~/.config/openbox/rc.xml` configuration file and set your config back
up from there with [Obconf](../ObConf/About.md) or by hand.

You can use the default configuration file, installed to
`/etc/xdg/openbox/rc.xml` if you use click-to-focus. However if you use
focus-follows-mouse, the `/usr/share/doc/openbox/rc-mouse-focus.xml`
file may make a better template for you to work with.

Take a look at the [details of the default
configuration](DefaultConfiguration.md) to learn what the
default keyboard bindings are.

## What's new in version 3.4 ?

Our [getting started guide](GettingStarted.md) is a great
place to start learning the best ways to start an Openbox session. If
you've been running a previous version of Openbox, you can keep using
the methods you have been and everything will work, but there are also
some new features that you may wish to take advantage of, especially in
terms of how you log into or run an Openbox session.

During the development cycle for Openbox 3.4, we fixed and closed every
bug listed in the bug tracker from previous versions. There's a big list
of the bugs in the [Changelog](../Changelog.md),
and we're not going to go through them all here. We're going to talk
about the new things.

### Usability

#### New log-in options

Openbox now provides three ways to start an Openbox session through a
graphical login manager, or through the command line. These new methods
to start Openbox are detailed in the [getting started guide](GettingStarted.md)
which you should definitely take a look at.

When logging in through KDM, GDM or some other graphical log-in system,
you no longer have to set up a `~/.xsession` file to get a usable Openbox session.
You can select the "Openbox" entry in the Session Type menu,
and support for various applications, as well as
[SCIM](#scim-support) are automatically included in your log in.
The `openbox-session` provides these same capabilities from the command line.
See the [autostart documentation](Autostart.md) to see how Openbox does this,
and how to launch your own choice applications along with Openbox when you log in.

Other new log-in options are the "KDE/Openbox" option, which opens a KDE session
with Openbox as your window manager and the "GNOME/Openbox" option which opens
a GNOME session with Openbox as your window manager.
These can also be accessed through the `openbox-kde-session` and
`openbox-gnome-session` commands.

See the [getting started guide](GettingStarted.md), even if Openbox is not new
to you, to see more about these startup options and what they provide -
especially the new "Openbox" (from graphical login) or `openbox-session` option.

#### New "Alt-Tab" dialog

![NewFocusDialog.png](../assets/img/NewFocusDialog.png)
Openbox 3.4 sports a brand new dialog for cycling between windows.
This new dialog shows icons for all windows you can switch to instead of just
showing the icon for the current target.
You can see the new dialog in action to the right.

The dialog shows when you press the Alt-Tab or Alt-Shift-Tab keys
in the default configuration.

#### Faster than ever

Openbox has always been fast, but version 3.4 is faster than any before it.
A large number of improvements were made throughout the code that impact directly
on how fast Openbox can do what it does. A couple examples would be the window
stacking code (how Openbox determines which windows to put on top of which)
and our use of lists.

#### More reliable

It's starting to sound like a Microsoft Windows ad, but in Openbox 3.4
we cleaned up a huge number of bug reports which had been sent in since
the last release. We also changed and rewrote a number of sections to improve
their reliability, such as the focus handling and session manager interaction.

#### Language support

Openbox now uses Pango exclusively for its font rendering, which means
better support for displaying text from all languages.

This change allowed us to clean up the font rendering code a lot, and
we've sped up the drawing routines significantly from previous Openbox versions.

#### Transparent windows

![TrueTransparentWindows.png](../assets/img/TrueTransparentWindows.png) Windows
that use the new 32-bit true transparency provided by x.org servers are
now supported by Openbox. You can see an example of urxvt running with
true transparency in the picture to the right.

True 32-bit transparency is made possible through the Composite
extension. So, in order to use this feature you need to run a composite
manager, such as this (run it without any arguments if you don't want
the extras like drop shadows):

```bash
xcompmgr -c -t-5 -l-5 -r4.2 -o.55 &
```

Openbox itself is not a composite manager, though it may be some day.

#### Keeping windows on screen

When windows adjust their dimensions, Openbox now takes care to make
sure they don't end up off of the screen, unless the application
explicitly requests it. This keeps your desktop more usable, meaning you
don't have to move windows around to use them so much, without
interfering with letting you move windows outside the screen if you want to,
like some other window managers do.

#### Improved startup notification

![KickerStartupNotification.png](../assets/img/KickerStartupNotification.png)
Openbox can now use startup notification when launching programs. This
means that when the application's window appears, Openbox will know when
you began launching the program, and what desktop you were launching it
on. It also means that other programs, such as taskbars, can show
feedback that an application is starting.

The [menu section](#startup-notification) talks about how to
use startup notification in your menus and key bindings.

Using startup notification for your menu entries also helps with focus
stealing prevention. If you use it, then Openbox can keep the launching
application's new window from stealing focus in the middle of your
typing (and sending your password off to IRC for example).

![NewBusyCursor.png](../assets/img/NewBusyCursor.png) Openbox used to use the
"watch" icon from the core X cursors when a program was starting up,
which is a very hard to use. This has been changed in 3.4 so that the
startup notification stays out of your way. If you use an Xcursors
theme, Openbox will use the busy cursor with an arrow, an example of
which can be seen to the left. And if you don't use an Xcursor theme, it
won't change your cursor at all.

#### Running applications remotely

![HostnameInTitlebar.png](../assets/img/HostnameInTitlebar.png) If you run
applications from another machine in your X session, Openbox will now
display their host machine in the window's titlebar, as you can see in
the image to the right.

#### Improved support for multiple screens

If you have a multi-monitor setup, either with Xinerama (a.k.a. Twin View)
or with independent screens, Openbox 3.4 has improved support for your setup.

Input focus handling has been made more robust all around in version
3.4, but especially with multiple screens in mind. Openbox will no
longer steal focus from other screens and you can click on the root
window to give focus to a particular screen, with a mouse binding. The
default configuration lets you focus a screen by clicking on the desktop
with your Left mouse button.

Window placement between Xinerama (a.k.a. Twin View) monitors has also
been improved. New windows will appear on the same monitor as other
windows they are related to. If they don't have related windows then
they are placed where the input focus is, or where the mouse pointer is.

#### Complete support for latest EWMH

Openbox 3.4 sports support for the freedesktop.org EWMH specification
(version 1.4-draft2), as well as even some hints which will be in a future release!

This means that most of the latest features from applications will have full
support from Openbox.

#### 8-bit TrueColor support

Environments such as VNC are often used in 8-bit display mode to reduce
the network bandwidth they require. VNC uses an 8-bit display mode
called "TrueColor", which previous versions of Openbox did not support.
As of version 3.4 you can use Openbox in these 8-bit TrueColor
environments, rather than forcing you to use the old "pseudocolor"
paradigm. This means that 8-bit VNC will work out of the box now.

#### Legacy fullscreen applications

Openbox can now detect when applications are trying to be fullscreen,
even when they don't use the EWMH fullscreen hints. This means that
applications, such as VLC (Video LAN Client) in fullscreen mode won't be
covered by panels or other windows.

#### Omnipresent windows

Omnipresent windows, or windows which are present across all desktops,
have had their behavior improved in Openbox 3.4. When changing desktops,
these windows will no longer "steal" focus and hold onto it.

#### Maximized terminal windows

Applications which resize in increments, such as x terminals have been
made to full the screen properly when they are maximized. This means
that when the window is maximized, you will no longer have a little
margin at the edge of the screen, where you can click and miss the
window. Some older terminal clients may not know what to do when they
are resized outside of their increments, but most will already work
fine, such as `xterm`, `rxvt-unicode`, and `gnome-terminal`.

#### Focus cycling to panels and desktop windows

![FocusCyclingToPanel.png](../assets/img/FocusCyclingToPanel.png) New options
have been added to the focus cycling actions to allow you to cycle between
panels and desktop windows. You can use Control-Alt-Tab to access this
feature in the default configuration. You can use these options with the
traditional focus cycling behavior or with the directional focus
cycling.

See the [configuration section](#nextwindow-and-directionalfocus-for-panels-and-desktop-windows)
for details on how to set this up in your own key bindings.

#### Session saving and restoring

Session saving and restoring has been revamped and improved in version 3.4.

Clients which do not use the session management protocol can now be
saved and restored. This applies to programs like `rxvt-unicode`, Firefox,
and probably most applications which are not GNOME or KDE based.

Ksmserver (KDE's session manager) allows the window manager to be more
precise in saving the session state. Openbox 3.4 takes advantage of this
feature to improve session saving within KDE.

#### Cycling across all desktops

![FocusCyclingForAllDesktops.png](../assets/img/FocusCyclingForAllDesktops.png)
An option has been added to allow you to focus cycle between windows on all
of your desktops. This is not enabled in the default configuration, but
you can easily add the `<allDesktops>` option to your NextWindow and
PreviousWindow actions to enable this behavior. For example, to get this
behavior in the default configuration you would change the Alt-Tab and
Alt-Shift-Tab key bindings to this:

```xml
<keybind key="A-Tab">
  <action name="NextWindow"><allDesktops>yes</allDesktops></action>
</keybind>
<keybind key="A-S-Tab">
  <action name="PreviousWindow"><allDesktops>yes</allDesktops></action>
</keybind>
```

When you use this, the desktop which the window is on is appended to the
window's title in the cycling dialog, as you can see in the image to the right.

This is also mentioned in the [configuration section](#nextwindow-for-all-desktops).

#### Desktop cycling dialog

In 3.4.4, the desktop cycling dialog's behavior has been changed again.
It will be shown for a fixed time whenever the desktop is changed,
instead of going away when the keys are released. This may or may not be
something which you like, but it is necessary at the moment for many
applications, such as Firefox. You can see the nitty gritty details as to why
[here](https://mail.gnome.org/archives/wm-spec-list/2007-May/msg00000.html).
But this change, along with some others, means that applications will
know when they do and don't have focus at all times, which will make
them work properly, which we think is a good thing.

If you don't want the dialog, or want to change the timeout, edit the
`<popupTime>` setting in the `<desktops>` setting, or use ObConf 2.0.3. Set
it to 0 to disable it completely:

```xml
<desktops>
  ... other settings ...
  <popupTime>400</popupTime>
</desktops>
```

Click here for information on
[versions 3.4.0 through 3.4.3](#desktop-cycling-dialog "TODO: versions not supported yet (?title=Help:UpgradingTo3.4&oldid=1209#desktop-cycling-dialog)")

#### Animated iconify and restore

A simple animation has been added for when windows are iconified or
restored to visually display where the window has been iconified.

You can watch this ![Video.png](../assets/img/Video.png)
[video showing the animation](../assets/video/IconifyAnimation.ogg) (in
ogg format), to have an idea of what it looks like. The animation is
very fast, so the video can only capture so much.

The animation is quick and not resource intensive. But if you prefer to
have your windows instantly appear and disappear, rather than animate,
you can use the `<animateIconify>no</animateIconify>` option in the
`<theme>` section of your configuration file.

#### Focus aware applications

Some applications like to track when they are focused or not, or which
of their windows is focused. Instant Messengers often do this, so that
it can alert you when a message comes and the window is not focused.
Firefox also uses these same mechanisms to tell which window the user is
working with.

Openbox 3.4 takes special care to make sure that applications always
know when their windows gain and lose focus. We mentioned one way that
we go about this in the [usability](#desktop-cycling-dialog)
section.

Right now the standards and coordination for this between window
managers and applications is non-existent, so Openbox takes every
precaution it can to make sure that every application will work right.

#### Resizing on the window's edges

Resizing grips have been added to all edges of your windows. These are
especially noticeable along the top edge of the titlebar, and in the
top-left and top-right corners. This makes resizing windows easier and
faster with just the mouse.

You can also resize along the bottom and side edges of the window,
though in most themes the sides are only a 1 pixel border, which can be
hard to click on.

If you undecorate a window (an option in the client menu), by default
the windows are given just a border. This border can now also be used to
resize the window.

In order to take advantage of these new resizing areas, however, you
need to have bindings for them in your configuration file. They are all
used in the default configuration. See the [configuration section](#new-contexts)
for what to add to your own configuration to get these to work for you.

Resizing any edge can also be accomplished with the Alt-Right mouse
button binding (in the default configuration).

#### Windows without icons

![IconlessWindows.png](../assets/img/IconlessWindows.png) Some applications don't
set an icon on their window. Generally, every application which would
show the window's icon will choose some icon of its own in this case. So
Openbox would show one thing, your task bar a different icon, and maybe
your pager would show a third icon, all for the same window.

Starting in Openbox 3.4, when a window does not provide any icon of its
own, Openbox will set its icon to a default "window" icon, so that
applications can agree on what to display for the window.

#### Synchronized window resizing

If your application supports it, Openbox 3.4 will synchronize its
resizing with the application to avoid excessive flicker.

You can, as always, also choose to have the application window not
resized until you have finished resizing the frame with the
`<drawContents>no</drawContents>` in the `<resize>` section
of your configuration file.

#### Improved "Show Desktop"

Many panels provide a button to "show your desktop". Openbox also
provides this functionality through the `Windows-D`<sup>1</sup> key
binding in the default configuration.

Show Desktop mode has been improved in Openbox 3.4. When you go in and
out of "Show Desktop" mode, Openbox will hide and show all your windows,
the same as it always has. But when you use "Show Desktop" mode to hide
all your windows and then open a new window, the other windows will be
iconified rather than unhidden. This makes "Show Desktop" a quick way to
unclutter your screen.

<sup>1</sup> The default bindings for the "Windows" key may not
work with your "Windows" key (if you have one), depending on your setup.
The "W" in modifier in key bindings is actually a shortcut for the
"Super" modifier key. Most distributions bind the "Super" modifier key
to the "Windows" key on 104-key PC keyboards, so this should just work
for most people.

Also see [the configuration section](#windows-key-in-key-bindings).

#### Key chain dialog

![KeychainDialog.png](../assets/img/KeychainDialog.png) Openbox has supported
emacs-style key chains for a long time. However, new in 3.4 is a small
popup dialog that visually shows you where you are in your key chain's
sequence.

The dialog is small and shows up in the top left corner of your screen
after a small delay. So if you go through your key chains without too
much waiting, you might never see it.

#### Chroot key chains and key quoting

Openbox 3.4 introduces the ability to "chroot" your keychains. This
means that when you enter a chroot section of your key chain, Openbox
will not leave the keychain automatically, and when you use keys further
along the chain, it will stay within the chroot.

There are a number of examples of how this could be used, so you can get
a better idea. You could use this to use the arrow keys to change
desktops, for instance. A key chain setup such as:

```xml
<keybind key="C-A-d" chroot="true">
  <keybind key="Up"><action name="DesktopUp"><dialog>no</dialog></action></keybind>
  <keybind key="Down"><action name="DesktopDown"><dialog>no</dialog></action></keybind>
  <keybind key="Left"><action name="DesktopLeft"><dialog>no</dialog></action></keybind>
  <keybind key="Right"><action name="DesktopRight"><dialog>no</dialog></action></keybind>
  <keybind key="Escape"><action name="BreakChroot"/></keybind>
</keybind>
```

This key chain would mean that when you pressed and released
Control-Alt-D, you would enter a chroot. From then on, other key
bindings would not function, but the Arrow keys by themselves would move
your around your desktops. Pressing Escape or Control-G (in the default
configuration) would take you back out of the chroot and return your key
bindings to normal.

Another use for chroots is "key quoting". This is used when you run an
Openbox session in a window, such as a VNC client. In order to use key
bindings inside the VNC, generally, you have to make sure that they are
different from the ones in your main Openbox session.

With key quoting, you can use the same key bindings in both. Here's an
example:

```xml
<keybind key="C-A-q" chroot="true">
  <keybind key="C-A-q"><action name="BreakChroot"/></keybind>
</keybind>
```

With this example, when you pressed Control-Alt-Q, Openbox would enter
the chroot. Then your normal Openbox key bindings would stop working and
would instead be passed through to the VNC session (assuming you have it
focused). When you were done, you could press Control-Alt-Q again, and
your normal key bindings would be restored in you main Openbox session.

The BreakChroot action is also new, and is just for breaking out of a
chroot. The global `<chainQuitKey>` (Control-G in the default
configuration) can also be used for this. However, the BreakChroot
action is special in that it will only break out of *one* chroot. So, if
you have nested chroots, you can break out of only as many as you want,
by placing 1 or more BreakChroot actions in a key binding.

The chroot changes are also talked about in the [configuration section](#chrooted-key-chains-and-breakchroot-action).

#### Auto-hiding decorations

![](../assets/img/HiddenTitlebarButtons.png) In Openbox
3.4 titlebar buttons can hide automatically. This is done in such a way
that they only hide if hiding won't move other buttons around. This way
you always know where to click to do the same thing, but when possible,
the buttons can be hidden to reduce clutter.

We've removed the <hideDisabled> option from the <theme> section of the
configuration file in favour of this auto-hiding. This is also mentioned
in the [configuration section](#hidedisabled-removed).

The bottom handle is also hidden automatically now for windows that
can't be resized, making their decorations cleaner and simpler.

#### MoveFromEdge actions

![MoveFromEdge.png](../assets/img/MoveFromEdge.png)
We added `MoveFromEdge*` actions corresponding to `MoveToEdge*` actions.
`MoveToEdge` actions let you move a window up against another window's edge
(or the edge of the screen). The new `MoveFromEdge` actions let you move a window
that is overlapping another off to its side. See the image to the right
for a graphical desciption of what these actions do.

**Note:** these have been rolled into the `MoveToEdge` actions in Openbox 3.4.3.

#### Moving maximized windows

If you have a multi-monitor system using Xinerama (a.k.a. TwinView),
you can now move maximized windows between your monitors without
unmaximizing them first. With the default configuration, just grab the
titlebar and drag to the other monitor, and the window will move there.

#### Root context for mouse bindings

A new "Root" context has been added for mouse bindings. This context is
for bindings on your desktop which you want to only function when you
aren't using some program to display icons on your desktop.

Generally this context is only used for showing root window menus. This
way, in the default configuration, when you have a desktop window in
place with icons (such as in GNOME or KDE), right clicking will bring up
the context menu for the desktop. And when you don't, right clicking
will bring up the Openbox root menu.

You can move the menu bindings from the "Root" context to the "Desktop"
context in your configuration file to have them work for both cases, if
you want to override the menus provided by the desktop icons.

This is also mentioned in the [configuration section](#new-root-context).

#### Helper windows

Openbox 3.4 improves how helper windows for applications behave. Helper
windows are those such as tear off toolbars and menus, and utility
windows like tool boxes.

If you are using an application across multiple desktops, when you focus
a main window, the helper windows will automatically come to that
desktop, so you don't need to move them all back and forth by hand.
Previously, it was so much effort as to be almost impossible to work
across desktops like this, such as having a gimp image open on different
desktops. But now, it's a snap.

Helper windows are also kept above the main window so that they are
always there when you need them. Toolbars and menus are also not given
focus when you click in them, so that you can keep on working in the
main window without having to click back to it.

When focus cycling, such as with Alt-Tab in the default configuration,
helper windows do not show up in the list when the main window is
already there. This reduces the clutter of focus cycling, letting you
choose the application itself easier. Once the application is focused,
however, you can use Alt-Tab to get to any of its helper windows.

#### Mangling desktop configuration

Changes to your desktop names or number in the Openbox configuration
will no longer be applied until the next time you run Openbox.
Restarting won't be enough to change them, you will have to log out of
your X session, and back in. The desktop names/number configuration
options are default values to be used when they are not already set by
other applications, or saved in your session.

This change was made so that if you change your desktop configuration
through a pager, Openbox will not clobber those settings when you
reconfigure it (to change your theme, for example). Also, since the
window manager is usually run before other applications on startup, they
can permanently manage your desktop configuration without Openbox
getting in the way.

[ObConf 1.6.2](../ObConf/About.md) will let you change these
settings in your config file, and will immediately update your current
session too, like a pager would, so that you don't need to log out and
in to see the changes.

#### --reconfigure option

Use the `openbox --reconfigure` command to tell the currently running
Openbox to reload its configuration. This will apply any changes to the
configuration file such as the theme or key bindings.

#### --restart option

Use the `openbox --restart` command to restart the current running
Openbox instance. This can be used to upgrade to a new version without
logging out of your session.

### Menus

#### Combined client list menu

![NewCombinedClientListMenu.png](../assets/img/NewCombinedClientListMenu.png) We've
added a new client list menu. Instead of having a submenu for each
desktop, it combines all your desktops into one menu. This menu is used
by middle click on the desktop in the default configuration.

To show this menu, put the following into a keyboard or mouse binding:

```xml
<action name="ShowMenu"><menu>client-list-combined-menu</menu></action>
```

For example, from the default configuration:

```xml
<mousebind button="Middle" action="Press">
  <action name="ShowMenu"><menu>client-list-combined-menu</menu></action>
</mousebind>
```

#### Iconified windows in the client list menus

Iconified windows in the client list menus used to be shown below a
separator. In Openbox 3.4 we have gotten rid of the visual clutter
created by that separator.

Instead, iconified windows will always appear at the bottom of the list
and will be surround with brackets. You can see, for example, that
Kaffeine Player is iconified in the picture of the [combined client list menu](#combined-client-list-menu).

#### Keyboard accelerators (using letters instead of arrows)

Wouldn't it be nice if you could just hit a letter to instantly choose
the item you wanted in your menus? Now you can!

In the [new client menu](#new-client-menu), the shortcuts are
highlighted with an underline. In other menus, underlines are not used,
instead you can just press the first letter of a menu item to jump to
it. If there are multiple entries with the same letter, press it again
to go to the second one.

If the first letter of a menu entry is not an ASCII alpha-numeric
character, then the first such character will be used as the shortcut
for that entry, and it will be underlined.

Now you can navigate your menus at light speed.

#### No more menu titles

We've had a large number of requests from users who wanted to get rid of
the titles at the top of their menus. So instead of just letting you
turn them on and off, we decided to give you a whole range of
flexibility.

Menus no longer have titles. So if you don't want a title, you don't
need one. But in their place you can now put headers (which look like
the old titles) anywhere you want in your menu. In the picture of the
[combined client list menu](#combined-client-list-menu)
above, there is a header for each desktop. You can do the same to
separate sections of your own menus.

The default menu that comes with Openbox puts a header at the top of the
menu, so it looks like the old menu title used to. Just remove the
separator item from the menu and it will no longer have a title.

You put these headers in your menu by using separators, but with a label
attribute, such as:

```xml
<menu id="root-menu" label="Openbox 3">
  <separator label="Openbox" />
</menu>
```

#### Startup notification

![](../assets/img/KickerStartupNotification.png "KickerStartupNotification.png")
Now when you run things from Openbox menus, you can enable startup
notification. This means that if you have a tasklist or some other
program that visually displays when applications are starting, it can
work from Openbox menus too.

It is, however, disabled by default because it shouldn't be used with
just anything. If you use it with an older terminal program, anything
you launch from the terminal will be given an old timestamp. One way to
fix that is to run `unset DESKTOP_STARTUP_ID` in your shell startup. You
also should not use it for commands that don't create a window on
screen, because without a window being created, nothing will know when
the command finished running.

To make use startup notification when launching a program use something
like the following in your menu:

```xml
<item label="Calculator">
  <action name="Execute">
    <startupnotify>
      <enabled>yes</enabled>
      <name>Calculator</name>
      <icon>gnome-calc2</icon>
    </startupnotify>
    <execute>gnome-calculator</execute>
  </action>
</item>
```

If you don't specify a `<name>` or `<icon>` field, they are derived from the
command that is being executed.

If the application starts, and the notification doesn't go away, that
means you shouldn't use it for that application. Any GNOME or KDE
application will support startup notification by default.

You can also use this startup notification when launching applications
with key bindings, in the same way.

The new startup notification feature is also mentioned in the
[usability section](#improved-startup-notification).

#### New client menu

![NewClientMenu.png](../assets/img/NewClientMenu.png) The client menu is the menu
you get when you right click on an application's title bar or click it icon
(in the default configuration).

The client menu has been restructured, revamped, and improved for Openbox 3.4.
You can see in the picture to the right, the new structure of the menu.
It's cleaner and easier to get to the item you want.

In addition, you can now use [keyboard accelerators](#keyboard-accelerators-using-letters-instead-of-arrows)
to navigate the menu.

As well, when you use a keyboard shortcut (Alt-space in the default configuration)
to bring up the menu, it will now pop up at the top left corner of the window,
rather than wherever your mouse pointer happens to be at the time.
You can see that happening in the picture also.

We've tried our best to make meaningful, unique keyboard shortcuts for all the
current translations of Openbox also, but any improvements would be appreciated.

#### Selecting disabled menu items

Disabled menu entries in the client menu can now be selected with the
mouse or the keyboard. Visually, this is a lot nicer feeling, when you
move the mouse around and the selected entry doesn't just disappear.

This also has the added bonus that no matter what entries in the menu
are enabled or disabled, the same number of arrow keys or letter keys
will always take you to the same entry. Yay for consistent behavior.

#### Menu placement

When you opened a menu close to the edge of the screen, opening
sub-menus used to push the whole menu back from the edge of the screen,
which could be jarring and make navigation difficult.

In Openbox 3.4, menus are always placed on screen such that they won't
have to move afterward. Sub-menus are opened cleverly to the side with
room available, so that the menus behave in a more predictable manner.

#### Large menus

![NewMoreMenu.png](../assets/img/NewMoreMenu.png) Menus that are bigger than your
screen is tall are no longer a problem for Openbox. When a menu grows too large,
it will be split off into a sub-menu at the bottom titled "More...".
You can see an example in the figure to the right.

### Themes

#### New default theme

![NewClearlooksTheme.png](../assets/img/NewClearlooksTheme.png) The Clearlooks and
Clearlooks-Olive themes by John McKnight have been added to the Openbox distribution.
These themes were designed to go well with the Clearlooks GTK theme (and
Klearlooks KDE theme). Clearlooks has been made the default theme for Openbox 3.4.

#### User specified fonts

Fonts are no longer loaded based on the theme. You specify your fonts
through the configuration file instead. However, font shadows are still
read from the theme, from the font string, the same way as before. For
new themes you can just include the shadow information in the font line,
such as:

```text
window.active.label.text.font: shadow=y:shadowtint=70:shadowoffset=1
```

The default configuration has fonts set up in it, which you can modify.
If you'd like to use your old configuration, the new version of [ObConf](../ObConf/About.md)
can set these for you or you can edit your configuration file by hand.

There are 5 different fonts used by Openbox: `ActiveWindow`, `InactiveWindow`,
`MenuHeader` (for [the new menu headers](#no-more-menu-titles)), `MenuItem`, and
`OnScreenDisplay` (for the various dialogs Openbox displays such as window cycling).

An example to set a font is:

```xml
<font place="ActiveWindow">
  <name>sans</name>
  <size>8</size>
  <weight>bold</weight>
  <slant>normal</slant>
</font>
```

You need one section like this for each of the above listed fonts, with the
`place` field changed appropriately. See the [configuration section](#new-fonts)
for the details of these configuration options.

#### Distributed themes renamed

The themes distributed with Openbox have been renamed to begin with a capital
letter. For example, the "syscrash" was renamed to "Syscrash" and the "bear2"
theme was renamed to "Bear2". If you use one of the default themes and your
configuration is not finding it after upgrading, this would be why.
This change makes the themes more consistant with other themes both in the
Openbox world and without.

#### New tricks for "ParentRelative" textures

![](../assets/img/NewParentrelativeTextures.png) In previous versions of Openbox,
parentrelative textures could not add any decorations of their own,
they had to only show through what was below them.

In Openbox 3.4 you can give parentrelative textures a border, bevel or interlacing,
just like any gradient or solid texture.

#### New theme elements for on-screen-displays

On-screen-displays such as the focus cycling (Alt-Tab) dialog, the
coordinates dialog, or the key chains dialog, can now be themed
independently. Previously, they just used the window title styles,
however, now you can set them however you wish. (They fall back to using
the window title styles as before.)

The new theme elements for on-screen-displays are:

- `osd.border.width` - The border width given to dialogs
- `osd.border.color` - The color of the border around dialogs
- `osd.bg` - The background for dialogs
- `osd.label.bg` - The background for text in dialogs
- `osd.label.text.color` - The text color for dialogs
- `osd.label.text.font` - The text shadow for dialogs
- `osd.hilight.bg` - The texture for the selected desktop in the
  desktop cycling dialog
- `osd.unhilight.bg` - The texture for non-selected desktops in the
  desktop cycling dialog

These are also all listed in the [theme specification](../Help/Themes.md).

#### New theme elements for toggled buttons

The toggled button theme elements have been split up into 3 elements for
each, so that each toggled state can be themed independently. You can
still use the old elements, and things will work the same as they did
previously, but you now have the option to theme toggled buttons with
much more attention to detail.

- `window.active.button.toggled.image.color` has been split into:
  - `window.active.button.toggled.unpressed.image.color`
  - `window.active.button.toggled.pressed.image.color`
  - `window.active.button.toggled.hover.image.color`
- `window.inactive.button.toggled.image.color` has been split into:
  - `window.inactive.button.toggled.unpressed.image.color`
  - `window.inactive.button.toggled.pressed.image.color`
  -` window.inactive.button.toggled.hover.image.color`
- `window.active.button.toggled.bg` has been split into:
  - `window.active.button.toggled.unpressed.bg`
  - `window.active.button.toggled.pressed.bg`
  - `window.active.button.toggled.hover.bg`
- `window.inactive.button.toggled.bg` has been split into:
  - `window.inactive.button.toggled.unpressed.bg`
  - `window.inactive.button.toggled.pressed.bg`
  - `window.inactive.button.toggled.hover.bg`

The Onyx themes, added to the distribution in Openbox 3.4.1 demonstrate
the uses of these new theme elements.

#### menu.border.color

The `menu.border.color` property has been added to the theme format.
This allows you to set the border color for Openbox menus independently
from that used for windows.

border.color has been obsoleted in 3.4, but is still used as a fallback
if the new border colors are not specified.

#### window.active.border.color

The `window.active.border.color` property has been added to the theme
format. This allows you to set the border color for the active
(currently focused) window. This color can be set independently for the
active and inactive windows now. See
[window.inactive.border.color](#windowinactivebordercolor).

Note that setting colors through globs such as `window.active.*.color`
may set this property for you when you didn't mean to. Themes which use
globbing like this may display differently in Openbox 3.4 than previous versions.

`border.color` has been obsoleted in 3.4, but is still used as a fallback
if the new border colors are not specified.

#### window.active.title.separator.color

![NewTitleSeparatorColors.png](../assets/img/NewTitleSeparatorColors.png)
The `window.active.title.separator.color` property has been added to the theme
format. This allows you to set the color for the titlebar border
(but only the section between the titlebar and the client) independently from
the rest of the borders. You can set this for both active an inactive windows.
See [window.inactive.title.separator.color](#windowinactivetitleseparatorcolor).

Note that setting colors through globs such as `window.active.*.color`
may set this property for you when you didn't mean to. Themes which use
globbing like this may display differently in Openbox 3.4 than previous versions.

#### window.inactive.border.color

The `window.inactive.border.color` property has been added to the theme
format. This allows you to set the border color for all inactive
(not currently focused) windows. This color can be set independently for the
active and inactive windows now. See [window.active.border.color](#windowactivebordercolor).

Note that setting colors through globs such as `window.inactive.*.color`
may set this property for you when you didn't mean to. Themes which use
globbing like this may display differently in Openbox 3.4 than previous versions.

border.color has been obsoleted in 3.4, but is still used as a fallback
if the new border colors are not specified.

#### window.inactive.title.separator.color

![NewTitleSeparatorColors.png](../assets/img/NewTitleSeparatorColors.png)
The `window.inactive.title.separator.color` property has been added to the
theme format. This allows you to set the color for the titlebar border
(but only the section between the titlebar and the client) independently from
the rest of the borders. You can set this for both active an inactive windows.
See [window.active.title.separator.color](#windowactivetitleseparatorcolor).

Note that setting colors through globs such as `window.inactive.*.color`
may set this property for you when you didn't mean to. Themes which use
globbing like this may display differently in Openbox 3.4 than previous versions.

#### menu.border.width

The `menu.border.width` property has been added to the theme format.
This allows you to set the border width used for Openbox menus
independantly from the border width used for windows.

#### menu.items.active.disabled.text.color

![](../assets/img/ActiveDisabledMenuEntry.png) The
`menu.items.active.disabled.text.color` property has been added to the
theme format. As of Openbox 3.4, disabled menu entries can still be
hilighted by the mouse or keyboard. This property lets you set the color
of the text for disabled entries when they are hilighted. Many themes
disabled text and selected colors are quite similar, so this can be used
to make the entries more readable. See the image on the right for an
example of a hilighted, but disabled, menu entry.

#### Even sized titlebar buttons

Previously titlebar buttons would be an arbitrary size based on the font
size you were using in the titlebar. In Openbox 3.4 the titlebar button
size has been standardized such that they will always be an even size.
This way, if you make even sized images for the buttons, you can know
that it will always be centered.

#### New default titlebar button images

![NewDefaultTitlebarButtons.png](../assets/img/NewDefaultTitlebarButtons.png)
The default images for the titlebar have been changed. They are probably
familiar since they appeared in many themes. Now they will be used for
any theme that doesn't provide its own images.

If you'd like to modify these images for your own themes, xbm copies of
the images are installed to `/usr/share/doc/openbox/xbm/`.

#### Improvements in the distributed themes

The distributed themes have been fixed up to work with all the latest features,
such as the [menu.items.active.disabled.text.color](#menuitemsactivedisabledtextcolor),
and the change in the border colors. None of them really take advantage
of these new features yet though, that's where you themers come in.

### Configuration

The following talks about changes to the Openbox configuration file.
This file is found in `~/.config/openbox/rc.xml` for users, and the system-wide
defaults are installed to `/etc/xdg/openbox/rc.xml`.

#### New contexts

There are five new contexts for mouse bindings, and if you don't include
them in your configuration file, they will not be used for anything.

The new contexts are: `Left`, `Right`, `TLCorner`, `TRCorner`, and `Top`.
These refer to the edges of windows, and the default configuration uses them
for resizing the window. Theese contexts can be used in the `<mouse>` section
of your configuration file. Here's what the default configuration has:

```xml
<mouse>
  ...

  <context name="Left">
    <mousebind button="Left" action="Press">
      <action name="Activate"/>
    </mousebind>
    <mousebind button="Left" action="Drag">
      <action name="Resize"><edge>left</edge></action>
    </mousebind>
  </context>

  <context name="Right">
    <mousebind button="Left" action="Press">
      <action name="Activate"/>
    </mousebind>
    <mousebind button="Left" action="Drag">
      <action name="Resize"><edge>right</edge></action>
    </mousebind>
  </context>

  <context name="TLCorner">
    <mousebind button="Left" action="Press">
      <action name="Activate"/>
    </mousebind>
    <mousebind button="Left" action="Drag">
      <action name="Resize"/>
    </mousebind>
  </context>

  <context name="TRCorner">
    <mousebind button="Left" action="Press">
      <action name="Activate"/>
    </mousebind>
    <mousebind button="Left" action="Drag">
      <action name="Resize"/>
    </mousebind>
  </context>

  <context name="Top">
    <mousebind button="Left" action="Press">
      <action name="Activate"/>
    </mousebind>
    <mousebind button="Left" action="Drag">
      <action name="Resize"><edge>top</edge></action>
    </mousebind>
  </context>

  ...
</mouse>
```

A new `Bottom` context has also been added, but in 3.4 it is just a synonym for
the `Handle` context. In future versions, the `Handle` context will be completely
replaced by the new `Bottom` context.

How these new contexts can be used and what they can do for you is
talked about more in the [usability section](#resizing-on-the-windows-edges).

#### New fonts

Fonts are now specified from your configuration file instead of by your
themes. The default configuration has fonts set up in it that you can modify.

There are 5 different fonts used throughout Openbox: `ActiveWindow`,
`InactiveWindow`, `MenuHeader`, `MenuItem`, and `OnScreenDisplay`.

`ActiveWindow` and InactiveWindow are used for window titlebars.
`MenuHeader` is used for the new [menu headers](#no-more-menu-titles). `MenuItem`
is used for the items in all Openbox menus. OnScreenDisplay is used for popup
dialogs such as the window cycling dialog shown by the Alt-Tab keys in the
default configuration.

The fonts are set in the `<theme>` section of your configuration file.
The default configuration has the following:

```xml
<theme>
  ...

  <font place="ActiveWindow">
    <name>sans</name>
    <size>8</size>
    <!-- font size in points -->
    <weight>bold</weight>
    <!-- 'bold' or 'normal' -->
    <slant>normal</slant>
    <!-- 'italic' or 'normal' -->
  </font>
  <font place="InactiveWindow">
    <name>sans</name>
    <size>8</size>
    <!-- font size in points -->
    <weight>bold</weight>
    <!-- 'bold' or 'normal' -->
    <slant>normal</slant>
    <!-- 'italic' or 'normal' -->
  </font>
  <font place="MenuHeader">
    <name>sans</name>
    <size>9</size>
    <!-- font size in points -->
    <weight>normal</weight>
    <!-- 'bold' or 'normal' -->
    <slant>normal</slant>
    <!-- 'italic' or 'normal' -->
  </font>
  <font place="MenuItem">
    <name>sans</name>
    <size>9</size>
    <!-- font size in points -->
    <weight>normal</weight>
    <!-- 'bold' or 'normal' -->
    <slant>normal</slant>
    <!-- 'italic' or 'normal' -->
  </font>
  <font place="OnScreenDisplay">
    <name>sans</name>
    <size>9</size>
    <!-- font size in points -->
    <weight>bold</weight>
    <!-- 'bold' or 'normal' -->
    <slant>normal</slant>
    <!-- 'italic' or 'normal' -->
  </font>
</theme>
```

This new font selection is also mentioned in the [usability section](#user-specified-fonts).

#### NextWindow for all desktops

The NextWindow and PreviousWindow actions have had the `<allDesktops>`
option added to them. The `<allDesktops>` option is a boolean value
(on/off/yes/no) which defaults to off. When you enable it, the action
will allow you to cycle through windows on all of your desktops.

Here is an example of using it:

```xml
<keybind key="A-Tab">
  <action name="NextWindow"><allDesktops>yes</allDesktops></action>
</keybind>
<keybind key="A-S-Tab">
  <action name="PreviousWindow"><allDesktops>yes</allDesktops></action>
</keybind>
```

The [usability section](#cycling-across-all-desktops) talks
more about this new feature and shows it in use.

#### NextWindow and DirectionalFocus for panels and desktop windows

The `NextWindow`, `PreviousWindow`, `DirectionalFocusNorth`,
`DirectionalFocusSouth`, `DirectionalFocusEast`, and `DirectionalFocusWest`
actions have had added to them the `<panels>` and `<desktop>` options. These
take boolean values (on/off/yes/no) and they both default to off.

When `<panels>` is enabled, the action will allow you to move focus to any
panel windows on screen. When `<desktop>` is enabled, the action will
allow you to move focus to your desktop window, if you have one. The
options can be combined to let you use one action to cycle through both,
as is done in Metacity. When either one is enabled, the action will no
longer go to regular windows.

In the default configuration, Control-Alt-Tab is bound to NextWindow
with both of these options enabled, which is similar to the default
bindings in Metacity. The default configuration has this:

```xml
<keyboard>
  ...

  <keybind key="C-A-Tab">
    <action name="NextWindow">
      <panels>yes</panels><desktop>yes</desktop>
    </action>
  </keybind>

  ...
</keyboard>
```

The [usability section](#focus-cycling-to-panels-and-desktop-windows)
talks about these new options.

#### Chrooted key chains and BreakChroot action

A new attribute called "chroot" has been added to the `<keybind>` element.
The chroot attribute is a boolean value (on/off/yes/no) which defaults off.
When it is enabled, the keybind is turned into a chroot.

Chrooting, what it means, and how to use it, is described in the
[usability section](#chroot-key-chains-and-key-quoting).

Any keybind can be made a chroot, even if there are no key bindings
chained within it. In that case the global `<chainQuitKey>` (Control-G by default)
will need to be used to exit the chroot. Chroots can also be nested within other
chroots for pretty much unlimited complexity if that's what you are after.

A new action `BreakChroot` has also been added which is only useful inside
of a chrooted key binding. This action breaks out of one level of chroot.
You can chain multiple `BreakChroots` together to break out of multiple levels
of chroots if you are nesting them.

Here's an example of a chroot key binding:

```xml
<keybind key="C-A-d" chroot="true">
  <keybind key="Up"><action name="DesktopUp"><dialog>no</dialog></action></keybind>
  <keybind key="Down"><action name="DesktopDown"><dialog>no</dialog></action></keybind>
  <keybind key="Left"><action name="DesktopLeft"><dialog>no</dialog></action></keybind>
  <keybind key="Right"><action name="DesktopRight"><dialog>no</dialog></action></keybind>
  <keybind key="Escape"><action name="BreakChroot"/></keybind>
</keybind>
```

#### New Root context

Another new context, above the Top, Left, Right, and so on, has been
added to Openbox 3.4. We've added a "Root" context which serves as a
context only for the root window. This means the mouse bindings in the
root context will only work if you're not using a desktop program for
icons, such as in GNOME and KDE. This allows us to put root menu
bindings in the default configuration without overriding the menus
provided by these desktop environments' desktops.

This new context is talked about and its uses decribed in the
[usability section](#root-context-for-mouse-bindings).

#### Windows key in key bindings

Key bindings that use `W` as a modifier key have changed. `W` used to be
hard-coded to be `Mod4Mask`. Now it has been changed to whatever mask you
have the `Super` mod key bound to.

You can use `xmodmap` to see your current bindings. Most modern
distributions bind the windows key to `Super_L`, and bind `Super_L` to
`Mod4Mask`. So this should probably not affect you unless you have a
highly customized system, or have customized your `xmodmap`.

#### hideDisabled removed

The `<hideDisabled>` option has been removed from the configuration file,
in favour of [auto-hiding decorations](#auto-hiding-decorations).

#### edges_hit_layers_below removed

The `<edges_hit_layers_below>` option has been removed from the
configuration file, in an effort to simplify and clarify our configuration.

#### Settings for specific windows ([Per-application settings](Applications.md))

##### Matching windows with wildcards

The per-application settings have been revamped for Openbox 3.4. When
specifying the name, class, or role for a rule, you can use simple
wildcard matching with the `*` and `?` characters. A `*` matches any
number of characters and a `?` matches any single character.

This means that the role has changed how it is matched. It used to just
match the first `n` characters, `n` was the length of the string you
provided. Now to get the same result, just append a `*` to the end of the role.

##### Matching against multiple rules

As well, multiple rules can be applied to the same window. This lets you
do more with less writing. For instance you could write one rule to
match against all windows and then later rules could further change
things for more specific windows. The rules are matched in the order
they appear in your configuration file, so later rules will override
previous rules if they both specify the same setting for a window.

##### Per-monitor positioning changed

The `<head>` parameter for positioning windows has been renamed to `<monitor>`.

##### The "default" value

You can now use "default" as the content for any option in a rule. This
is the same as the option not being present at all.
