# Contents

Welcome to the community maintained documentation for Openbox!
Please help out and add your own articles or improve the ones that are already here.

In order to get full access and contribute in the wiki,
all you need to do is prove you are a person. Please see [RequestWriteAccess](#).

## rc.xml

### [Configuration](Configuration.md)

The configuration documentation has details on the various options you can set in `rc.xml`.

### [Application settings](Applications.md)

Customize properties such as borders, geometry, workspace presence, layering etc.
on a per-application basis.

### Mouse & keybindings

#### [Binding documentation](Bindings.md)

Improve productivity and customize the function of your desktop
by binding actions to key/mouse buttons (commonly called hot keys).

#### [Actions](Actions.md)

Comprehensive documentation of all actions available for key and mouse bindings
and the options which can affect their behavior.

## Menus

### [Menu documentation](Menus.md)

Describes how to set up your own menus in Openbox.

### [Actions](Actions.md#introduction)

The actions documentation lists all of the actions available for use in Openbox menus.

### [Pipe menus](Menus.md#pipe-menus)

The pipe menu documentation explains basic use of pipe menus in Openbox.
If you're looking for scripts there are many available [on the community page](../Community/Pipemenus/index.md).

### Generating an applications menu

- Scripts may be used to generate an application menu based
  on the contents of `/usr/share/applications` or other directories.
  See [this section](../Community/Pipemenus/index.md#application-menus) for a complete list.
- There are also instructions available for getting
  a [working Debian menu](MenusDebian.md), if yours is not.

## Themes

### [Theme specification](Themes.md)

Comprehensive detail and documentation all of the elements found in an Openbox theme.

### [Openbox 3.4 theme file changes](UpgradingTo3.4.md#themes)

- Details differences between 3.3-&gt;3.4 theme files
- A tool to help with [converting blackbox/fluxbox themes](https://icculus.org/openbox/tools/themeupdate.py)
  to Openbox themes. (For non-xpm-based themes.)

## Desktop Environments

### [Openbox in GNOME](UsingOpenboxInGNOME.md)

Instructions for running Openbox in the GNOME desktop environment
and getting things to work how you want.

### [Openbox in KDE](UsingOpenboxInKDE.md)

Instructions for running Openbox in K Desktop Environment.

### [Openbox in XFCE](UsingOpenboxInXFCE.md)

Instructions for running Openbox in the XFCE desktop enviroment.

## Custom Desktop Environments

### [openbox-session](Session.md)

Running Openbox as a stand-alone window manager in part of a custom desktop environment.

### [Autostart](Autostart.md)

The autostart documentation gives instructions on how to launch programs
with Openbox at startup (not applicable unless openbox-session is called
from the Desktop Manager/`xinit`)

## Miscellaneous

### rc.xml Configuration examples

- [rc.xml Configuration reference](DefaultConfiguration.md) -
  Lists all default key bindings and default configuration.
- [Focus-follows-mouse](MouseFocusExample.md) -
  This configuration is similar to the default configuration,
  but has more suitable mouse bindings for focus-follows-mouse
  that won't interfere with your windows' stacking order.
- [Vi-styled bindings](ClaysViStyleSpatial.md) -
  Two examples of Vi-style keybindings (by [Clay Barnes](../User/Rcbarnes.md)).
- ["Windows"/Super key control](WindowsInteractionWithWindowsKey.md) - Example
  of using the "Windows" AKA. Super key to control windows (by Deters).
- [Irssi-style window switching](IrssiStyleFocus.md)

### [Feature list](Features.md)

A list of features found in the Openbox windowmanager.

### [Frequently asked questions](../FAQ.md)

### [Compiling from source](Installing.md)

Details what you need to build the latest version of Openbox,
and how to install it correctly.

### [Using Git](UsingGit.md)

Explains how to get bleeding-edge Openbox code for testing or developing with.

### [ObConf](../ObConf/About.md)

`Obconf` provides a simple graphical user interface to ease configuration
for new Openbox users.

### [Upgrading to 3.4](UpgradingTo3.4.md)

Walks through all the changes made since version 3.3, and there is a lot of them.
Some of them mean new configuration options and features available to you,
that you need to update your configuration to access.

## Other resources

[The Arch wiki](https://wiki.archlinux.org/index.php/Openbox)
has a lot of great information on setting up and using Openbox.

Many Openbox questions have been answered in forums around the internet.
Trying a search may be fruitful.

See [community portal](../Community/Portal.md) for other community resources
and related projects.
