# Actions

## Older versions

This page describes Openbox 3.6.
~~For older documentation, see `/wiki/?title=Help:Actions&oldid=3651 3.5` and
`/wiki/?title=Help:Actions&oldid=2410 3.4`.
The syntax described there should still work in 3.6.
If you have an older config that doesn't work in 3.6, please let us know.~~

## Introduction

Actions are used both in [key and mouse bindings](Bindings.md) and in [menus](Menus.md).

## Action syntax

Actions are specified with the `<action>` tag as follows:

```xml
<action name="NAME">
  OPTIONS
</action>
```

NAME is the name of the action as listed below,
OPTIONS is a set of tags specific to each action also defined below.

## Global actions

These actions are not used to manipulate windows.
As such, they work whether a window is currently focused or not.

### Execute

Runs a program.

| Option      | Default Value | Description
| ---         | ---           | ---
| `<command>` | ""            | A string which is the command to be executed, along with any arguments to be passed to it. The `~` tilde character will be expanded to your home directory, but no other shell expansions or scripting syntax may be used in the command unless they are passed to the `sh` command. Also, the `&` character must be written as `&` in order to be parsed correctly. `<execute>` is a deprecated name for `<command>`.
| `<prompt>`  | none          | A string which Openbox will display in a popup dialog, along with "Yes" and "No" buttons. The execute action will only be run if you choose the "Yes" button in the dialog.

#### Startup notification

You can use the startup notification protocol to tell everyone that an
application is starting up. This can be used with most applications, but
should **not** be used with old-style xterminals such as `xterm`, `urxvt`,
`aterm`, etc, unless you include the command
**`unset DESKTOP_STARTUP_ID`** in your shell's `~/.zshrc`, `~/.bashrc`
or equivalent startup script.

Startup notification has these options, which are included inside the
Execute action, in a `<startupnotify>` tag:

| Option      | Default Value | Description
| ---         | ---           | ---
| `<enabled>` | no            | A boolean (yes/no) which says if the startup notification protocol should be used to notify other programs that an application is launching. This is disabled by default to avoid it being used for old-style xterminals.
| `<wmclass>` | none          | A string specifying one of the values that will be in the application window's WM_CLASS property when the window appears. This is not needed for applications that support the startup-notification protocol.
| `<name>`    | none          | The name of the application which is launching. If this option is not used, then the command itself will be used for the name.
| `<icon>`    | none          | The icon of the application which is launching. If this option is not used, then the command itself will be used to pick the icon.

Example:

```xml
<keybind key="W-t">
  <action name="Execute">
    <command>urxvt</command>
  </action>
</keybind>

<keybind key="W-space">
  <action name="Execute">
    <startupnotify>
      <enabled>yes</enabled>
      <name>Terminal</name>
      <icon>konsole</icon>
    </startupnotify>
    <command>gnome-terminal</command>
  </action>
  <action name="Execute">
    <prompt>Are you sure you want to run a calculator!?</prompt>
    <startupnotify>
      <enabled>yes</enabled>
      <name>Calculator</name>
      <wmclass>xcalc</wmclass>
    </startupnotify>
    <command>xcalc</command>
  </action>
</keybind>
```

### ShowMenu

Shows a menu by name.

| Option       | Default Value | Description
| ---          | ---           | ---
| `<menu>`     | ""            | The name of the menu to be shown. Names of menus are specified in the menu file, in the `id` attribute of the `<menu>` tag.
| `<position>` |               | Show the menu in the specified position on the specified monitor, see below.

The position tag has three sub-tags that are similar to how the
per-application position tag works. `<x>` and `<y>` specify a position and
take either a pixel value, the string "center" which will center the
menu in that dimension, or a relative value specified either as a
percentage or ratio. A relative value is interpreted in terms of the
monitor the menu will be shown on, and will be relative to the left/top
edge of the menu window and monitor for positive values, and to the
right/bottom edge for negative values. The `<monitor>` tag can take one of
the following values: *default* which is the default, this is also the
same as specifying *primary* at present, and means the menu will show up
on the primary monitor; *mouse* is the monitor containing the mouse
pointer; *active* is the monitor containing the focused client, or the
primary monitor if no client has focus; *all* will make the positions be
relative to the full workspace area; any integer between 1 and the
number of monitors you have will place the menu on the monitor with that number.

Openbox provides a number of built-in menus:

- `client-list-combined-menu` - A list of all windows, across all
  desktops
- `client-list-menu` - A list of all windows, separated into sub menus
  by desktop
- `client-menu` - A menu to control a window, such as to maximize or iconify it
  - This menu will only show with a key binding if an application window
    is focused, and for mouse bindings if the mouse event was on an
    application window (or its decorations).
- `client-send-to-menu` - A list of desktops. When one is selected,
  the window is sent to the desktop.
  - This menu will only show with a key binding if an application window
    is focused, and for mouse bindings if the mouse event was on an
    application window (or its decorations).
- `client-layer-menu` - A menu for selecting the stacking layer for a window,
  to put it "always on top" for example.
  - This menu will only show with a key binding if an application window
    is focused, and for mouse bindings if the mouse event was on an
    application window (or its decorations).

In addition, the default configuration provides this menu in the `menu.xml` file:

- `root-menu` - An example menu containing some applications and options
  for controlling Openbox

Example:

```xml
<keybind key="A-space">
  <action name="ShowMenu">
    <menu>client-menu</menu>
  </action>
</keybind>

<mousebind button="Right" action="Press">
  <action name="Activate"/>
  <action name="ShowMenu">
    <menu>client-menu</menu>
  </action>
</mousebind>

<mousebind button="Middle" action="Press">
  <action name="ShowMenu">
    <menu>client-list-combined-menu</menu>
  </action>
</mousebind>

<mousebind button="Right" action="Press">
  <action name="ShowMenu">
    <menu>root-menu</menu>
  </action>
</mousebind>

<keybind key="W-x">
  <action name="ShowMenu">
    <menu>programs</menu>
    <position>
      <x>center</x>
      <y>center</y>
      <monitor>1</monitor>
    </position>
  </action>
</keybind>
```

### NextWindow

Cycles focus to the next window.

| Option           | Default Value                                         | Description
| ---              | ---                                                   | ---
| `<dialog>`       | list                                                  | Specifies the type of dialog to be shown on screen with icons for all the windows which can be focused. Choices are `list`, `icons`, or `none`. If `none` is selected then no dialog will be shown.
| `<bar>`          | yes                                                   | A boolean (yes/no) which specifies if the focus indicator is shown which highlights the window that will be focused.
| `<raise>`        | no                                                    | A boolean (yes/no) which specifies if windows are temporarily raised to the front while cycling through them.
| `<allDesktops>`  | no                                                    | A boolean (yes/no) which when enabled lets you cycle focus between windows on all desktops, instead of only on the current desktop.
| `<panels>`       | no                                                    | A boolean (yes/no) which when enabled lets you cycle focus to/between panel windows such as your taskbar. This can be combined with `<desktop>`.
| `<desktop>`      | no                                                    | A boolean (yes/no) which when enabled lets you cycle focus to the desktop window, if one exists (such as in GNOME or KDE). This can be combined with `<panels>`.
| `<linear>`       | no                                                    | A boolean (yes/no) which when enabled causes focus to cycle in a fixed ordering, rather than in the order which windows have been last focused.
| `<interactive>`  | yes                                                   | A boolean (yes/no) which when disabled causes the action to immediately switch focus to the next target.
| `<finalactions>` | [Focus](#focus), [Raise](#raise), [Unshade](#unshade) | A list of actions to run on the window which the user finally selects using this action.

Example:

```xml
<keybind key="A-Tab">
  <action name="NextWindow"/>
</keybind>
<keybind key="C-A-Tab">
  <action name="NextWindow">
    <panels>yes</panels>
    <desktop>yes</desktop>
  </action>
</keybind>
<keybind key="W-Tab">
  <action name="NextWindow">
    <finalactions>
      <action name="Focus"/>
      <action name="Raise"/>
      <action name="Unshade"/>
      <action name="MoveResizeTo">  <!-- center the window which we're focusing -->
        <x>center</x>
        <y>center</y>
      </action>
    </finalactions>
  </action>
</keybind>
```

### PreviousWindow

Cycles focus to the previous window. Takes the same options as [NextWindow](#nextwindow).

### DirectionalCycleWindows

Cycles focus to the window in the direction specified of the currently
focused window.

| Option           | Default Value                                         | Description
| ---              | ---                                                   | ---
| `<direction>`    | north                                                 | Which direction to cycle focus in. Can be "north", "northeast", "east", "southeast", "south", "southwest", "west" or "northwest".
| `<dialog>`       | yes                                                   | A boolean (yes/no) which specifies if a dialog is shown on screen with the name and icon of the window which will be focused.
| `<bar>`          | yes                                                   | A boolean (yes/no) which specifies if the focus indicator is shown which highlights the window that will be focused.
| `<raise>`        | no                                                    | A boolean (yes/no) which specifies if windows are temporarily raised to the front while cycling through them.
| `<finalactions>` | [Focus](#focus), [Raise](#raise), [Unshade](#unshade) | A list of actions to run on the window which the user finally selects using this action.
| `<panels>`       | no                                                    | A boolean (yes/no) which specifies whether panel windows are to be selectable.
| `<desktops>`     | no                                                    | A boolean (yes/no) which specifies whether desktop windows are to be selectable.

Example:

```xml
<keybind key="W-Up">
  <action name="DirectionalalCycleWindows"><direction>north</direction><dialog>yes</dialog></action>
</keybind>
<keybind key="W-S-Down">
  <action name="DirectionalFocus">
    <direction>south</direction>
    <finalactions>
      <action name="Focus"> <!-- give focus without raising the window -->
      <action name="Unshade">
    </finalactions>
  </action>
</keybind>
```

### DirectionalTargetWindow

Moves focus to the window in the direction specified of the currently
focused window. This is similar to the
[DirectionalFocusCycle](#directionalfocuscycle) action, but it moves focus instantly
instead of letting you interactively choose a window.
Takes the same options except for `<dialog>` and `<bar>`.

Example:

```xml
<keybind key="W-Up">
  <action name="DirectionalTargetWindow"><direction>north</direction></action>
</keybind>
<keybind key="W-S-Down">
  <action name="DirectionalTargetWindow">
    <direction>south</direction>
    <finalactions>
      <action name="Focus"> <!-- give focus without raising the window -->
      <action name="Unshade">
    </finalactions>
  </action>
</keybind>
```

### GoToDesktop

Changes the visible desktop.

| Option   | Default Value | Description
| ---      | ---           | ---
| `<to>`   | current       | The desktop to switch to, starting from 1, or one of the following special values: "current", "next", "previous", "last", "north" or "up", "south" or "down", "west" or "left", "east" or "right".
| `<wrap>` | yes           | A boolean (yes/no) which when enabled lets you wrap around from the last desktop to the first, west to east, north to south, etc, and vice versa.

The value "last" for the `<to>` option goes to the desktop you were on
before the current one. Only one desktop is remembered, but there is a
timeout so that if you go past a few desktops, you will go to the one
you were really on before. This is useful if you switch between two
desktops by going to the next or previous desktop several times, for
example with the scroll wheel. The timeout is 750ms and cannot be
configured currently.

Example:

```xml
<keybind key="W-F1">
  <action name="GoToDesktop"><to>1</to></action>
</keybind>
<keybind key="W-BackSpace">
  <action name="GoToDesktop"><to>last</to></action>
</keybind>
<keybind key="W-A">
  <action name="GoToDesktop"><to>next</to><wrap>no</wrap></action>
</keybind>
```

### AddDesktop

Create a new desktop in the location specified.

| Option    | Default Value | Description
| ---       | ---           | ---
| `<where>` | last          | Can be `current` (add a new desktop in front of the current one and shuffle the desktops after it over) or `last` (add a new desktop after the last one).

```xml
<keybind key="W-F12">
  <action name="AddDesktop">
    <where>current</where>
  </action>
</keybind>
```

### RemoveDesktop

Remove the a desktop in the location specified and move the windows on
it to the one after it (or before if the removed desktop is the last one).

| Option    | Default Value | Description
| ---       | ---           | ---
| `<where>` | last          | Can be `current` (remove the current desktop and shuffle the desktops after it over) or `last` (remove the last desktop). |

Example

```xml
<keybind key="W-F11">
  <action name="RemoveDesktop"/>
</keybind>
```

### ToggleShowDesktop

Hides all windows so that the desktop is visible, and gives focus to
the desktop window if one exists (such as in GNOME and KDE). You can also use
the action again to show the windows again, if no windows have become visible yet.

| Option     | Default Value | Description
| ---        | ---           | ---
| `<strict>` | "no"          | A boolean (yes/no) which specifies if windows are allowed to show themselves while in Show Desktop mode. In strict mode, they cannot.

```xml
<keybind key="W-d">
  <action name="ToggleShowDesktop"/>
</keybind>
```

### ToggleDockAutohide

Toggles the autohide setting on the dock temporarily.
This effectively means you can show/hide the dock with a keybinding.

Example:

```xml
<keybind key="C-A-d">
  <action name="ToggleDockAutohide"/>
</keybind>
```

### Reconfigure

Prompts Openbox to reload its config file, menu and theme.

Example:

```xml
<keybind key="W-F11">
  <action name="Reconfigure"/>
</keybind>
```

### Restart

Restarts Openbox. This starts a new copy of Openbox, and can be used to upgrade
to a newly installed version without logging out of your X session.
It can also be used to start another window manager.

| Option      | Default Value | Description
| ---         | ---           | ---
| `<command>` | ""            | A string which is the command to be executed as the new window manager, along with any arguments to be passed to it.

Example:

```xml
<keybind key="W-F12">
  <action name="Restart"/>
</keybind>
<keybind key="W-F11">
  <action name="Restart"><command>firebox</command></action>
</keybind>
```

### Exit

Exits Openbox.

If Openbox is built with session support and is running inside a session manager
(such as gnome-session, ksmserver), then Openbox will ask the session manager
to log out. Otherwise, Openbox will simply exit, ending the current X session.

| Option     | Default Value | Description
| ---        | ---           | ---
| `<prompt>` | true          | A boolean (yes/no) which specifies if Openbox should display a prompt dialog asking if you really want to exit before it actually exits.

Example:

```xml
<keybind key="C-A-S-F12">
  <action name="Exit">
    <prompt>yes</prompt>
  </action>
</keybind>
```

### SessionLogout

This is a synonym for the [Exit](#exit) action.

### Debug

Prints out a string in Openbox's output for debugging purposes.

| Option     | Default Value | Description
| ---        | ---           | ---
| `<string>` | ""            | The string to be printed out.

Example:

```xml
<keybind key="W-F10">
  <action name="Debug">
    <string>-------------------------------</string>
  </action>
</keybind>
```

## Window actions

These actions are used to control windows. For key bindings, they
operate on the currently focused window. For mouse bindings they operate
on the window being clicked/dragged on.

### Focus

Focuses a window.

Example:

```xml
<mousebind button="A-Left" action="Press">
  <action name="Focus"/>
  <action name="Raise"/>
</mousebind>
```

### Raise

Raises a window above other windows in its layer.

Example:

```xml
<mousebind button="A-Left" action="Press">
  <action name="Focus"/>
  <action name="Raise"/>
</mousebind>
```

### Lower

Lowers a window below other windows in its layer.

Example:

```xml
<mousebind button="A-Middle" action="Press">
  <action name="Lower"/>
  <action name="FocusToBottom"/>
  <action name="Unfocus"/>
</mousebind>
```

### RaiseLower

Raises the window if it is currently behind any other windows in its layer.
Lowers the window if it is above all other windows in its layer.

Example:

```xml
<keybind key="C-A-r">
  <action name="RaiseLower"/>
</keybind>
```

### Unfocus

Move focus off of the window. Usually used in conjuction with [FocusToBottom](#focustobottom).

Example:

```xml
<mousebind button="A-Middle" action="Press">
  <action name="Lower"/>
  <action name="FocusToBottom"/>
  <action name="Unfocus"/>
</mousebind>
```

### FocusToBottom

Move the window to the bottom of the recently-used-windows list.
This means that other windows will be given preference when selecting which
window to focus. Usually used in conjuction with [Unfocus](#unfocus).

Example:

```xml
<keybind key="A-Escape">
  <action name="Lower"/>
  <action name="FocusToBottom"/>
  <action name="Unfocus"/>
</keybind>
```

### Iconify

Iconify (a.k.a. minimize) the window.

Example:

```xml
<mousebind button="Left" action="Click">
  <action name="Iconify"/>
</mousebind>
```

### Close

Close the window.

Example:

```xml
<keybind key="A-F4">
  <action name="Close"/>
</keybind>
```

### ToggleShade

Shade (a.k.a. Roll up) the window, so only its titlebar is visible.
If the window is already shaded, then Unshade (a.k.a. Roll down) the window.

Example:

```xml
<mousebind button="Left" action="Click">
  <action name="ToggleShade"/>
</mousebind>
```

### Shade

Shade (a.k.a. Roll up) the window, so only its titlebar is visible.

Example:

```xml
<mousebind button="Up" action="Click">
  <action name="Shade"/>
  <action name="FocusToBottom"/>
  <action name="Unfocus"/>
</mousebind>
```

### Unshade

Unshade (a.k.a. Roll down) the window, when it has been [shaded](#shade).

Example:

```xml
<mousebind button="A-Left" action="Click">
  <action name="Unshade"/>
</mousebind>
```

### ToggleOmnipresent

Make the window visible on all desktops, if it is not already.
Otherwise, make it visible only on the current desktop.

Example:

```xml
<mousebind button="Left" action="Click">
  <action name="ToggleOmnipresent"/>
</mousebind>
```

### ToggleMaximize

Maximize the window to fill the entire screen in the directions specified.
If it is already maximized, return it to its original dimensions.

| Option        | Default Value | Description
| ---           | ---           | ---
| `<direction>` | both          | The direction to maximize the window, can be `both`, `horizontal` or `vertical`.

Example:

```xml
<mousebind button="Left" action="Click">
  <action name="ToggleMaximize"/>
</mousebind>
<mousebind button="Middle" action="DoubleClick">
  <action name="ToggleMaximize"><direction>horizontal</direction></action>
</mousebind>
```

### Maximize

Maximize the window to fill the entire screen in the directions
specifed.

| Option        | Default Value | Description
| ---           | ---           | ---
| `<direction>` | both          | The direction to maximize the window, can be `both`, `horizontal` or `vertical`.

Example:

```xml
<keybind key="A-F6">
  <action name="Maximize"/>
</keybind>
```

### Unmaximize

Unmaximizes the window in the directions specified, and return it to its
pre-maximized dimensions.

| Option        | Default Value | Description
| ---           | ---           | ---
| `<direction>` | both          | The direction to maximize the window, can be `both`, `horizontal` or `vertical`.

Example:

```xml
<keybind key="A-F7">
  <action name="Unmaximize"/>
</keybind>
```

### ToggleFullscreen

Makes the window fullscreen, filling the entire monitor, without any decorations.
If the window is already fullscreened, then it returns it to its pre-fullscreen dimensions.

Example:

```xml
<keybind key="A-F12">
  <action name="ToggleFullscreen"/>
</keybind>
```

### ToggleDecorations

Removes the window's decorations. If the `<keepBorder>` configuration
option is enabled (as in the default configuraton), then a border will
be left as the only decorations around the window. If the window has
already had its decorations removed, then this will restore them.

Example:

```xml
<keybind key="A-S-d">
  <action name="ToggleDecorations"/>
</keybind>
```

### Decorate

Gives a window its normal decorations.

Example:

```xml
<keybind key="C-S-d">
  <action name="Decorate"/>
</keybind>
```

### Undecorate

Removes decorations from a window. If the `<keepBorder>` configuration
option is enabled (as in the default configuraton), then a border will
be left as the only decorations around the window.

Example:

```xml
<keybind key="C-S-d">
  <action name="Undecorate"/>
</keybind>
```

### SendToDesktop

Moves the window to another desktop.

| Option     | Default Value | Description
| ---        | ---           | ---
| `<to>`     | current       | The desktop to send the window to, starting from 1, or one of the following special values: `current`, `next`, `previous`, `last`, `north` or `up`, `south` or `down`, `west` or `left`, `east` or `right`.
| `<wrap>`   | yes           | A boolean (yes/no) which when enabled lets you wrap around from the last desktop to the first, west to east, north to south, etc, and vice versa.
| `<follow>` | yes           | A boolean (yes/no) which when enabled will also switch to the specified desktop.

Example:

```xml
<keybind key="W-S-F1">
  <action name="SendToDesktop"><to>1</to></action>
</keybind>
<keybind key="W-S-BackSpace">
  <action name="SendToDesktop"><to>last</to></action>
</keybind>
<!-- Cycle through all windows and focus the selected one on the current desktop -->
<keybind key="W-S-Tab">
  <action name="NextWindow">
    <allDesktops>yes</allDesktops>
    <finalactions>
      <action name="SendToDesktop"><to>current</to></action>
      <action name="focus"/>
      <action name="raise"/>
    </finalactions>
  </action>
</keybind>
```

See also [GoToDesktop](#gotodesktop).

### Move

Begin interactively moving the window. Once a move has begun, you can move
the window either by moving the mouse pointer, or by using the arrow keys.
The move will complete when you release a mouse button, or press the Enter key.
Pressing Escape will cancel the move.

Example:

```xml
<mousebind button="A-Left" action="Drag">
  <action name="Move"/>
</mousebind>
```

### Resize

Begin interactively resizing the window. Once a resize has begun, you can resize
the window either by moving the mouse pointer, or by using the arrow keys.
The move will complete when you release a mouse button, or press the Enter key.
Pressing Escape will cancel the move.

If the resize is bound to a mouse button, then the corner/edge of the window
that is resized is chosen by which is nearest to the mouse pointer. You can use
the `<edge>` option to override this and specify which corner/edge should be resized.

| Option   | Default Value | Description
| ---      | ---           | ---
| `<edge>` | none          | One of: `top`, `left`, `right`, `bottom`, `topleft`, `topright`, `bottomleft`, `bottomright`. This specifies which corner/edge should be resized, and overrides having the edge determined dynamically by which is closest to the mouse pointer.

Example:

```xml
<mousebind button="A-Right" action="Drag">
  <action name="Resize"/>
</mousebind>
```

### MoveResizeTo

Move and/or resize a window.

| Option      | Default Value | Description
| ---         | ---           | ---
| `<x>`       | current       | The position to move the window to. `current` specifies the window's current x-position. `center` moves the window to the center of the screen, horizontally. A number gives the absolute position to move the window to. A negative value specifies the distance from the right edge of the screen (e.g. `-2` is 2 pixels in from the right edge). Use `+-` to specify a negative position relative to the left edge (e.g. `+-10` is 10 pixels off the screen on the left side), and `--` to specify a negative position relative to the right edge (e.g. `--5` is 5 pixels off the screen on the right side).
| `<y>`       | current       | The position to move the window to. `current` specifies the window's current y-position. `center` moves the window to the center of the screen, vertically. A number gives the absolute position to move the window to. A negative value specifies the distance from the bottom edge of the screen (e.g. `-2` is 2 pixels in from the bottom edge). Use `+-` to specify a negative position relative to the top edge (e.g. `+-10` is 10 pixels off the top of the screen), and `--` to specify a negative position relative to the bottom edge (e.g. `--5` is 5 pixels off the bottom of the screen).
| `<width>`   | current       | The width to resize the window to. `current` specifies the window's current width. A number specifies the desired width of the window. You may also specify the width as a fraction or a percentage, eg `50%` or `7/8`. If `client="yes"` is specified as an attribute, then the size determines the size of the application window inside the decorations. The default includes the decorations in the size.
| `<height>`  | current       | The height to resize the window to. `current` specifies the window's current height. A number specifies the desired height of the window. You may also specify the width as a fraction or a percentage, eg `50%` or `7/8`. If `client="yes"` is specified as an attribute, then the size determines the size of the application window inside the decorations. The default includes the decorations in the size.
| `<monitor>` | current       | The monitor to move the window to (in Xinerama/TwinView setups with multiple monitors). `current` specifies the window's current monitor. `all` specifies to use all monitors together. `next` specifies to move the window to the next monitor relative to the one it is currently on. `prev` specifies to move the window to the previous monitor relative to the one it is currently on. A number specifies the desired monitor (starting from 1).

Example:

```xml
<keybind key="W-2">
  <action name="MoveResizeTo">
    <!-- move the window to the second monitor -->
    <monitor>2</monitor>
  </action>
</keybind>
<keybind key="W-F10">
  <action name="MoveResizeTo">
    <!-- put the window in the bottom right corner -->
    <x>-0</x>
    <y>-0</y>
  </action>
</keybind>
<keybind key="W-c">
  <action name="MoveResizeTo">
    <!-- center the window on the first monitor -->
    <x>center</x>
    <y>center</y>
    <monitor>1</monitor>
  </action>
</keybind>
<keybind key="C-A-1">
  <action name="MoveResizeTo">
    <!-- adjust a window's height -->
    <width client="yes">1/2</width>
    <height>300</height>
  </action>
</keybind>
```

### MoveRelative

Move the window by an incremental amount, relative to its current
position

| Option   | Default Value | Description
| ---      | ---           | ---
| `<x>`    | 0             | The amount to move the window in the horizontal direction. A positive value moves it to the right, and a negative value moves it to the left.
| `<y>`    | 0             | The amount to move the window in the vertical direction. A positive value moves it down, and a negative value moves it up.

Example:

```xml
<keybind key="W-Right">
  <action name="MoveRelative">
    <x>5</x>
    <y>0</y>
  </action>
</keybind>
<keybind key="W-Up">
  <action name="MoveRelative">
    <x>0</x>
    <y>-5</y>
  </action>
</keybind>
```

### ResizeRelative

Resize the window by an incremental amount, relative to its current
size.

| Option     | Default Value | Description
| ---        | ---           | ---
| `<left>`   | 0             | The amount to resize the left edge of the window by. A positive value moves the left edge to the left, growing the window. A negative value moves the edge to the right, shrinking the window.
| `<right>`  | 0             | The amount to resize the right edge of the window by. A positive value moves the right edge to the right, growing the window. A negative value moves the edge to the left, shrinking the window.
| `<top>`    | 0             | The amount to resize the top edge of the window by. A positive value moves the top edge up, growing the window. A negative value moves the edge down, shrinking the window.
| `<bottom>` | 0             | The amount to resize the bottom edge of the window by. A positive value moves the bottom edge down, growing the window. A negative value moves the edge up, shrinking the window.

Example:

```xml
<keybind key="W-Down">
  <action name="ResizeRelative">
    <bottom>5</bottom>
  </action>
</keybind>
<keybind key="W-S-Down">
  <action name="ResizeRelative">
    <bottom>-5</bottom>
  </action>
</keybind>
```

### MoveToEdge

Moves the window to the nearest edge in the direction specified.
Edges are the outer edges of other windows, monitor edges in multi-monitor setups,
or the desktop boundaries.

| Option        | Default Value | Description
| ---           | ---           | ---
| `<direction>` | north         | The direction to move the window, can be `north`, `south`, `west` or `east`.

Example:

```xml
<keybind key="W-Left">
  <action name="MoveToEdge"><direction>west</direction></action>
</keybind>
```

### GrowToEdge

Grows the window until it touches the nearest edge in the direction
specified. Edges are the outer edges of other windows, monitor edges in
multi-monitor setups, or the desktop boundaries. If the window edge is
at the screen edge already, it is [shrunk](#shrinktoedge) instead.

| Option        | Default Value | Description
| ---           | ---           | ---
| `<direction>` | north         | The direction to grow the window, can be `north`, `south`, `west` or `east`. |

Example:

```xml
<keybind key="C-Right">
  <action name="GrowToEdge"><direction>west</direction></action>
</keybind>
```

### GrowToFill

Grows the window in every direction but doesn't go across any edges
until all edges touch something else.

### ShrinkToEdge

Shrinks the window until it touches the nearest edge in the direction
specified. Edges are the outer edges of other windows, monitor edges in
multi-monitor setups, or the desktop boundaries. If no edge is found,
the window is halved in size.

| Option        | Default Value | Description
| ---           | ---           | ---
| `<direction>` | north         | The direction to shrink the window, can be `north`, `south`, `west` or `east`. |

Example:

```xml
<keybind key="C-Right">
  <action name="GrowToEdge"><direction>west</direction></action>
</keybind>
```

### If

This action allows you to do different things depending on various
conditions. The basic structure is:

```xml
<action name="If">
  <query target="default">
    <somecondition>value of condition</somecondition>
    <someothercondition>value of condition</someothercondition>
  </query>
  <then>
    ... list of <action>s to run when true
  </then>
  <else>
    ... list of <action>s to run when false
  </else>
</action>
```

The query tag's target can be either `default` or `focus`, and multiple
query tags can be present in one If action. `default` means to check the
conditions against whatever window the actions would normally act on,
while `focus` always checks against the window that currently has focus.
These differ for example during focus cycling actions, or when the
`ForEach` action is being used.

The list of conditions is:

<table>
<thead><tr>
<th style="width:50%">Condition</th>
<th style="width:50%">Description</th>
</tr></thead><tbody>
<tr><td><code>&lt;shaded&gt;</code></td>
  <td>yes/no: if the window is rolled up or not.</td>
</tr>
<tr><td><code>&lt;maximized&gt;</code></td>
<td>yes/no</td>
</tr>
<tr><td><code>&lt;maximizedhorizontal&gt;</code></td>
<td>yes/no</td>
</tr>
<tr><td><code>&lt;maximizedvertical&gt;</code></td>
<td>yes/no</td>
</tr>
<tr><td><code>&lt;iconified&gt;</code></td>
<td>yes/no: if the window is minimized or not.</td>
</tr>
<tr><td><code>&lt;focused&gt;</code></td>
<td>yes/no: the window is the focused window.
This may not be true while focus cycling or in the finalactions of focus cycling.
</td></tr>
<tr><td><code>&lt;urgent&gt;</code></td><td>
yes/no: the window has the urgent flag set
(also known as <code>DEMANDS_ATTENTION</code>).</td>
</tr>
<tr><td><code>&lt;undecorated&gt;</code></td>
<td>yes/no: if the window decorations are hidden or not.</td>
</tr>
<tr><td><code>&lt;omnipresent&gt;</code></td>
<td>yes/no: if the window is visible on all desktops or not</td>
</tr>
<tr><td><code>&lt;activedesktop&gt;</code></td>
<td>The desktop that is currently active. This can only be a number.</td>
</tr>
<tr><td><code>&lt;desktop&gt;</code></td>
<td>The desktop the client is currently on. This can be the number of a desktop
or the special values <code>current</code> or <code>other</code>.</td>
</tr>
<tr><td><code>&lt;monitor&gt;</code></td>
<td>Matches the monitor the client is currently on
(most area wins if spanning several).</td>
</tr>
<tr><td><code>&lt;title&gt;</code> or <code>&lt;title type="pattern"&gt;</code></td>
<td>A wildcard pattern to match against the window title,
like <code>* - Mozilla Firefox</code>.</td>
</tr>
<tr><td><code>&lt;title type="regex"&gt;</code></td>
<td>As above, but use regex instead of wildcard pattern,
e.g.: <code>- Mozilla Firefox$</code>.</td>
</tr>
<tr><td><code>&lt;title type="exact"&gt;</code></td>
<td>As above, but the string must match exactly (case sensitive).</td>
</tr>
<tr><td><code>&lt;class&gt;</code>, <code>&lt;name&gt;</code>,
<code>&lt;role&gt;</code>, <code>&lt;type&gt;</code></td>
<td>Works like the <code>&lt;title&gt;</code> tag and takes the type parameter,
but matches against the window class, name, role and type respectively.</td>
</tr></tbody></table>

Example:

```xml
<!-- this corresponds to the ShadeLower and UnshadeRaise actions from 3.4 -->
<mousebind button="Up" action="Click">
  <action name="If">
    <query>
      <shaded>yes</shaded>
    </query>
    <then>
      <action name="Lower"/>
    </then>
    <else>
      <action name="Shade"/>
    </else>
  </action>
</mousebind>
<mousebind button="Down" action="Click">
  <action name="If">
    <query>
      <shaded>no</shaded>
    </query>
    <then>
      <action name="Raise"/>
    </then>
    <else>
      <action name="Unshade"/>
    </else>
  </action>
</mousebind>
```

### ForEach

This action has the same syntax as the `If` action,
but runs for every client window on every desktop, not just the current window.

### Stop

As of Openbox 3.6.1: `Stop` will end execution only of the parent element
that directly contains the `Stop`. If a grandparent element exists (via
hierarchical nesting via `If` or `ForEach`), execution of that grandparent
element will (surprisingly!) continue. Additionally, if a `ForEach`
contains an `If` (or several nested Ifs), and if one of those Ifs contains
a `Stop`, then that `Stop` will cause that `ForEach` to exit once the current
iteration completes.

As of Openbox 3.6.1: If a parent `ForEach` contains a child `ForEach` that
contains a `Stop`, Openbox may permanently lock up and freeze. This is a bug.

`Stop` takes no arguments.

One pattern is to use a `Stop` at the end of a `ForEach`. In this pattern,
the actions in the `ForEach` will be applied only to the first client that
matches the `ForEach`'s query.

### ToggleAlwaysOnTop

Makes the window always above other windows, in the "always on top"
layer. If the window is already set to be above other windows, this puts
the window back in the stacking order with normal windows.

Example:

```xml
<keybind key="W-F8">
  <action name="ToggleAlwaysOnTop"/>
</keybind>
```

### ToggleAlwaysOnBottom

Makes the window always below other windows, in the "always on bottom"
layer. If the window is already set to be below other windows, this puts
the window back in the stacking order with normal windows.

Example:

```xml
<keybind key="W-F5">
  <action name="ToggleAlwaysOnBottom"/>
</keybind>
```

### SendToLayer

Moves the window to the specified layer.

| Option    | Default Value | Description
| ---       | ---           | ---
| `<layer>` | normal        | The layer to put the window in. It can be the `top` layer, which appears over all other windows except fullscreen windows, the `normal` layer, or the `bottom` layer, which appears below all other windows.

```xml
<keybind key="W-F7">
  <action name="SendToLayer"><layer>top</layer></action>
</keybind>
```

<style>
  th:nth-of-type(1){width:25%;}
  th:nth-of-type(2){width:10%;}
  th:nth-of-type(3){width:65%;}
</style>
