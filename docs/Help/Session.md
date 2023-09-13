# Session

It is entirely possible to run Openbox as a standalone window manager
alongside modular components to completely replicate the functionality
of more heavyweight/resource intensive Desktop Environments such as
Gnome, KDE or XFCE. There is even a Desktop Environment
([LXDE](UsingOpenboxInLXDE.md)) built around Openbox.

## Power management

Tips for [Power management](PowerManagement.md) and
[Suspend and Hibernate](SuspendAndHibernate.md).

## Menu Generation

[Pipe menus](../Community/Pipemenus/index.md) are applications that
dynamically generate your Openbox menu. They can provide a dynamic
applications menu, system information, amongst other fun things.
See [here](../Community/Pipemenus/index.md) for more information, and to download them.

## Panels, widgets, desktops, pagers, etc..

Besides the programs included in GNOME and KDE...

- [Avant Window Navigator](https://github.com/p12tic/awn/)
  "(AWN/Awn) is a dock-like navigation bar for the linux desktop that positions
  itself at the bottom of the screen. It can be used to keep track of
  open windows and behaves like a normal window list."
- [BBDock](https://bbdock.nethence.com/) "BBDock is an application
  launcher for Blackbox (and others) that allows you to create
  application buttons in the slit/dock. It works with PNG files rather
  than XPM images. It supports alpha blending at 16, 24 and 32 bits
  color-depth. Also, the raise-window function is available to window
  managers which implement the EWMH specification." (untested. EWMH
  capable) Tested by CrossWind, Fully operational!
- [bbtools](https://sourceforge.net/projects/bbtools/) "BB-tools are a number of
  simple X-Window programs to display the status of different resources.
  The style and part of the code is copied from Blackbox a
  small and extremely fast X11-Windowmanager."
- [bmpanel2](https://code.google.com/archive/p/bmpanel2/)
  "Nice NETWM-compatible panel for X11."
- [conky](https://github.com/brndnmtthws/conky/) "Conky is a free,
  light-weight system monitor for X, that displays any information on
  your desktop. Conky is licensed under the GPL and runs on Linux and
  BSD."
- [fbpanel](https://fbpanel.sourceforge.net//) "fbpanel is a
  lightweight, NETWM compliant desktop panel. It works with any NETWM
  compliant window manager (e.g. xfwm4, sawfish, openbox, metacity,
  kde wm)"
- [feh](https://feh.finalrewind.org/) An image viewer with many
  features.
- [flauncher](https://sourceforge.net/projects/flauncher/) "The project
  is intendent to replace the common panels (top panel and bottom
  panel in Gnome). It gives speedup of application management reducing
  the distance of mouse movements." (An attempt to get the panel
  functionality into a separate window.)
- [gDesklets](https://launchpad.net/gdesklets/) "gDesklets is a system for
  bringing mini programs (desklets), such as weather forecasts, news
  tickers, system information displays, or music player controls, onto
  your desktop, where they are sitting there in a symbiotic
  relationship of eye candy and usefulness. The possibilities are
  really endless and they are always there to serve you whenever you
  need them, just one key-press away. The system is not restricted to
  one desktop environment, but currently works on most of the modern
  Unix desktops (including GNOME, KDE, Xfce)."
- [iDesk](https://idesk.sourceforge.net/html/index.html)
  "iDesk gives users of minimal wm's (fluxbox, blackbox, openbox, windowmaker...)
  icons on their desktop. The icon graphics are either from a png or svg (vector)
  file and support some eyecandy effects like transparency. Each icon
  can be confgured to run one or more shell commands and the actions
  which run those commands are completely configurable. In a nutshell
  if you want icons on your desktop and you don't have or dont't want
  KDE or gnome doing it, you can use iDesk."
- [kooldock](https://store.kde.org/p/1081070/)
  "A kool dock for KDE. It attemps to resemble the Mac OSX dock."
- [LXPanel](https://github.com/lxde/lxpanel/)
- [nitrogen](https://github.com/l3ib/nitrogen/) "Nitrogen is a
  background browser and setter for X windows. It is written in C++
  using the gtkmm toolkit. It can be used in two modes: browser and
  recall. Nitrogen has been in development for over 2 years, due to
  real life and laziness. For more info, check out the features
  section."
- [Oboinus](https://github.com/jaalto/oboinus/) "X11 background
  previewer and setter."
- [ObPager](https://obpager.sourceforge.net/) "OBPager is a lightweight
  pager designed to be used with NetWM-compliant window managers like
  OpenBox. Unlike many other pagers out there, OBPager has very few
  dependencies, requiring only Xlib and glibc++ (no Gnome or KDE
  necessary)."
- [perlpanel](https://github.com/bbidulock/perlpanel/) "PerlPanel is
  an attempt to build a useable, lean panel program (like Gnome's
  gnome-panel and KDE's Kicker) in Perl, using GTK 2. It has an
  object-oriented design for easy customisation and extension, and an
  applet architecture that means that you can create an applet in a
  matter of minutes."
- [pypanel](https://pypanel.sourceforge.net/) "PyPanel is a lightweight
  panel/taskbar written in Python and C for X11 window managers. It
  can be easily customized to match any desktop theme or taste.
  PyPanel works with EWMH compliant WMs (Openbox, PekWM, FVWM, etc.)
  and is distributed under the GNU General Public License v2."
- [PyTyle](https://pytyle.com) "PyTyle is a manual tiling manager that
  can slide into any EWMH compliant window manager, inspired by
  XMonad. It will allow you to enable/disable tiling on a per screen
  per workspace basis, and continually tile your windows."
- [ROX Desktop](https://rox.sourceforge.net/desktop/) "ROX
  is a fast, user friendly desktop which makes extensive use of
  drag-and-drop. The interface revolves around the file manager, or
  filer, following the traditional Unix view that \`everything is a
  file' rather than trying to hide the filesystem beneath start menus,
  wizards, or druids. The aim is to make a system that is well
  designed and clearly presented. The ROX style favours using several
  small programs together instead of creating all-in-one
  mega-applications."
- [Screenlets](http://www.screenlets.org/) "Screenlets are small
  owner-drawn applications (written in Python) that can be described
  as "the virtual representation of things lying/standing around on
  your desk". Sticknotes, clocks, rulers, ... the possibilities are
  endless."
- [Screenpager](https://ostatic.com/screenpager) "Screenpager is a
  screenwise pager for X workstations running Xinerama. It works like
  a desktop pager, but acts at the level of screens. Instead of paging
  the desktop as a whole, it can page each screen independently, or
  move pages from screen to screen."
- [Set Layout](../dist/tools/setlayout.c) A small program to set your desktops
  into a grid if you do not use a pager.
- [stalonetray](https://kolbusa.github.io/stalonetray/) "Stalonetray is a
  stand-alone freedesktop.org and KDE system tray (notification area)
  for X Window System/X11 (e.g. X.Org or XFree86). It has full XEMBED
  support and minimal dependencies: an X11 lib only. Stalonetray works
  with virtually any EWMH-compliant window manager."
- [Super Karamba](https://netdragon.sourceforge.net/ssuperkaramba.html)
  "SuperKaramba is, in simple terms, a tool that allows you to easily
  create interactive eye-candy on your KDE desktop."
- [SuperSwitcher](https://code.google.com/archive/p/superswitcher/)
  "SuperSwitcher is a (more feature-ful) replacement for the Alt-Tab
  window switching behavior and Ctrl-Alt-Left/Right/Up/Down workspace
  switching behavior that is currently provided by Metacity."
- [tint2 panel/taskbar](https://gitlab.com/o9000/tint2)
  "tint2 is a simple panel/taskbar unintrusive and light (memory / cpu / aestetic)."
- [visibility-python](http://code.l3ib.org/?p=visibility-python.git;a=summary)
  "gtk2 x11 pager / window list." (click snapshot to download a .tar.gz)
- [wbar](https://github.com/rodolf0/wbar)
  "wbar is a quick launch bar. It's developed with speed in mind and is highly tweakable."
- [wmctrl](https://www.freedesktop.org/wiki/Software/wmctrl/)
  "wmctrl is a UNIX/Linux command line tool to interact with
  an EWMH/NetWM compatible X Window Manager".
  Example of changing number of desktops:
```bash
wmctrl -n 4
```
- [xfce4-panel](https://www.xfce.org/) "The Xfce panel supports
  multiple panels, with many options for their position, appearance,
  transparency and behavior. There are many items available by default
  to customize your panels, like application launchers with detachable
  menus, a graphical pager, a tasklist, a clock, a system tray, a
  show/hide desktop switcher, and even more."
- [xprop](https://www.x.org/archive/X11R7.5/doc/man/man1/xprop.1.html)
  is utility for displaying and changing X server window and font
  properties. To change number of columns and rows of desktops grid layout run:
```bash
xprop \
  -root \
  -format _NET_DESKTOP_LAYOUT 32c \
  -set _NET_DESKTOP_LAYOUT <orientation>,<columns>,<rows>,<starting_corner>
```
where `<orientation>` is «0» or «1»; `<starting_corner>` is «0», «1», «2» or
«3»; `<columns>, <rows>` - number of columns and rows respectively
([more](https://standards.freedesktop.org/wm-spec/1.3/ar01s03.html)).
Example:
```bash
xprop \
  -root \
  -format _NET_DESKTOP_LAYOUT 32c \
  -set _NET_DESKTOP_LAYOUT 0,2,2,0
```
- [ksuperkey](https://github.com/hanschen/ksuperkey) (daemon) uses
  XTEST extension to bind the modifier key (like ctrl, alt (meta),
  windows (super)) to any shortcut (like Alt+F1).
```bash
  ~/.config/openbox/rc.xml
```
```xml
<keybind key="A-F1">
    <action name="ShowMenu">
      <menu>root-menu</menu>
    </action>
</keybind>
```
```bash
  ~/.config/openbox/autostart
```
```bash
  ksuperkey -e 'Super_L=Alt_L|F1' &
```
This allow you to open Openbox menu using super (windows) key.
- [xdotool](https://www.semicomplete.com/blog/geekery/headless-wrapper-for-ephemeral-xservers/)
  "lets you simulate keyboard input and mouse activity, move and resize windows, etc.
  It does this using X11's XTEST extension and other Xlib functions".
```bash
# focus and raise xterm window
xdotool \
    search \
      --maxdepth 2 \
      --onlyvisible \
      --all \
      --name xterm \
    windowfocus \
    windowraise

# open Openbox menu, when mouse in top-left corner
# (Alt+F1 must be bind to open root-menu)
xdotool \
    behave_screen_edge \
      --delay 300 \
      --quiesce 3000 \
      top-left \
    key "Alt_L+F1"
```
- [xkb-switch](https://github.com/ierton/xkb-switch) "is a C++ program
  that allows to query and change the XKB layout state". Example of
  using "Win+space" to switch keyboard layout:
```bash
~/.config/openbox/rc.xml
```
```xml
<keybind key="W-space">
    <action name="Execute">
      <command>xkb-switch --next</command>
    </action>
</keybind>
```

## Other links

You can find lots of dockapps at [dockapps.windowmaker.org](https://www.dockapps.net/).
Some nice ones are «wmCalClock», «wmnd», «wmix» and «wmpinboard».

There are other programs of interest in the [community portal](../Community/Portal.md).
