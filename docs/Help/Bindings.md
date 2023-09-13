# Bindings

Key and mouse bindings are created in your `~/.config/openbox/rc.xml` file.
You should copy the file from `/etc/xdg/openbox/rc.xml`
to `~/.config/openbox/rc.xml` to edit it, if that file does not already exist.

Key bindings and mouse bindings both use
[Actions](Actions.md) to specify what they will do. There are a *lot* of actions
available to you. Here we'll talk about how to write a generic key binding,
or mouse binding. See the [actions documentation](Actions.md) for details
about what actions are available to use and their varied options.

## Key bindings

Key bindings are found in the `<keyboard>` section of your `rc.xml`
configuration file. Any bindings outside of that section are not valid
and will be ignored.

Here are a few example key bindings from the default configuration file,
to give us an idea of what we'll be talking about:

```xml
<keyboard>
  <keybind key="A-F4">
    <action name="Close"/>
  </keybind>
  <keybind key="A-Escape">
    <action name="Lower"/>
    <action name="FocusToBottom"/>
    <action name="Unfocus"/>
  </keybind>
  <keybind key="A-space">
    <action name="ShowMenu"><menu>client-menu</menu></action>
  </keybind>
</keyboard>
```

### Syntax

A key binding is specified as follows:

```xml
<keyboard>
  ...
  <keybind key="KEY-COMBINATION...">
    ...ACTIONS...
  </keybind>
  ...
</keyboard>
```

### Key combination

**KEY-COMBINATION** is the key combination which you want to bind to the
actions. The format for the **KEY-COMBINATION** is: `Modifier-Modifier-Key`.
Any number of modifiers (0 or more) can be used together,
and they are each separated by a "-". Multiple **KEY-COMBINATION**
can be specified in one keybind by separating them with spaces.
This is useful if you use multiple keybinds
for a thing that is quite complicated to specify.

### Modifiers

| Modifier keys | Description
| ---           | ---
| S             | Shift key
| C             | Control key
| A             | Alt key
| W             | Super key (Usually bound to the Windows key on keyboards which have one)
| M             | Meta key
| H             | Hyper key (If it is bound to something)

You can also use `Mod1` through `Mod5` as the modifiers to directly select
a modifier mask (e.g. `Mod1` to select `Mod1Mask`), but this is for advanced users
who have customized their modifier mapping with `xmodmap`.

### Keys

The **Key** is the name of the key, such as "a", "space", "Escape",
"less", or "F1". You can find the name of any key by using the `xev`
command in a terminal, pressing the desired key, and watching the output
from `xev` in the terminal. For example, the following `xev` output
indicates, on the third line, that the **Menu** key was pressed.

```text
KeyRelease event, serial 36, synthetic NO, window 0x1e00001,
  root 0x7e, subw 0x0, time 29920856, (168,-7), root:(900,313),
  state 0x0, keycode 135 (keysym 0xff67, Menu), same_screen YES,
  XLookupString gives 0 bytes:
  XFilterEvent returns: False
```

This key can then be used as in the following example.

```xml
<keyboard>
  ...
  <keybind key="C-Menu S-F10">
    <action name="ShowMenu">
      <menu>root-menu</menu>
    </action>
  </keybind>
  ...
</keyboard>
```

Keys can also be specified by their numeric codes. This can be done by
specifying the keycode in hex. To take the above example, the keycode
for the **Menu** key is **135**, which is **0x87** in hexadecimal.
This can then be used:

```xml
<keyboard>
  ...
  <keybind key="C-0x87">
    <action name="ShowMenu">
      <menu>root-menu</menu>
    </action>
  </keybind>
  ...
</keyboard>
```

Note that the "0x" prefix is required to interpret the key as a numeric keycode,
and that the hex characters are case-insensitive (i.e. you can use "0xAE" or "0xae").

### Actions

The **ACTIONS** can be any number of [actions](Actions.md).
They will generally be executed in order from the first to the last.

### Key chains

You can create Emacs-style key chains simply by nesting key bindings
inside each other. Here's an example:

```xml
<keybind key="C-f">
  <keybind key="x">
    <action name="ToggleMaximizeFull"/>
  </keybind>
  <keybind key="s">
    <action name="ToggleShade"/>
  </keybind>
</keybind>
```

In order to maximize a window using this key binding you would press the
Control key and the "f" key together (which is written as C-f), then you
would release everything and press the "x" key.

To shade a window, you would press Control and the "f" key together, and
then release everything and press the "s" key.

You can create key chains within key chains, with as many levels as you
want, if you wish to.

### The key chain dialog

![KeychainDialog.png](../assets/img/KeychainDialog.png) When you start a key chain,
after a short delay, a small dialog will appear in the top left corner
of the screen to show you where you are in the key chain.

As long as you are in a key chain, other key bindings will not work
except the ones found inside the key chain.

### Cancelling key chains

If you leave Openbox in a key chain state for too long without
completing it, Openbox will cancel the key chain and restore your normal
key bindings.

You can also use the "C-g" (Control key and "g" key together), in the
default configuration, to cancel any key chain which you are in. The
choice of this key is controlled by the `<chainQuitKey>` in the `<keyboard>`
section of the `rc.xml` configuration file.

The default `<chainQuitKey>` is defined as this:

```xml
<keyboard>
  <chainQuitKey>C-g</chainQuitKey>
  ...
</keyboard>
```

### Chrooting key chains

By default, once you get to the terminal end of a key chain, and run
some actions with it, Openbox will exit the key chain and return to the
normal key bindings. With a "chrooted" key chain, Openbox will not leave
the key chain automatically, and when you use keys further along the
chain, it will stay within the chroot.

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

Once you enter a chrooted key chain, Openbox will not time out and leave
the chain. You will remain inside the key chain until you use a
*BreakChroot* action, as shown here, or press the
[`<chainQuitKey>`](#cancelling-key-chains). `BreakChroot` actions
are different from the `<chainQuitKey>` in that they will only break out
of *one* chroot. So, if you have nested chroots, you can break out of only
as many as you want, by placing 1 or more `BreakChroot` actions in a key binding.

### Key quoting with Chroots

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

### Creating hotkeys from the command line

[OBHotkey](https://obhotkey.sourceforge.net) lets you add/remove key
bindings from the command line.

## Mouse bindings

Mouse bindings are used to bind [Actions](Actions.md) to mouse events.
These are used to control and define most of Openbox's interactive behavior,
from what happens when you drag a window's titlebar,
to when you press a window's Close button.

Mouse bindings are found in the `<mouse>` section of your `rc.xml`
configuration file. Any bindings outside of that section are not valid
and will be ignored.

![Important.png](../assets/img/Important.png) It is highly recommended
that you build any custom mouse bindings from those in the default configuration,
or the [mouse-focus example](MouseFocusExample.md), rather than starting from
nothing, as they are rather intricate and have some advanced but subtle
features.

To get us started, here are a few example mouse bindings from the
default configuration file:

```xml
<mouse>
  <context name="Titlebar">
    <mousebind button="Left" action="Press">
      <action name="Focus"/>
      <action name="Raise"/>
    </mousebind>
    <mousebind button="Left" action="Click">
      <action name="Unshade"/>
    </mousebind>
    <mousebind button="Left" action="Drag">
      <action name="Move"/>
    </mousebind>
    <mousebind button="Left" action="DoubleClick">
      <action name="ToggleMaximizeFull"/>
    </mousebind>

    <mousebind button="Up" action="Click">
      <action name="Shade"/>
      <action name="FocusToBottom"/>
      <action name="Unfocus"/>
    </mousebind>
    <mousebind button="Down" action="Click">
      <action name="Unshade"/>
    </mousebind>
  </context>
</mouse>
```

### Syntax

A mouse binding is specified as follows:

```xml
<mouse>
  ...
  <context name="CONTEXT...">
    <mousebind button="BUTTON..." action="EVENT">
      ...ACTIONS...
    </mousebind>
  </context>
  ...
</mouse>
```

Any number of `<mousebind>`s may appear within a `<context>`, and any number
of [Actions](Actions.md) may appear within a `<mousebind>`.

### Context

Mouse bindings, unlike key bindings, are made within **contexts**.
The **CONTEXT** represents what you are clicking/dragging on with your mouse
(with the exception of the special `MoveResize` context). You can create
identical mousebinds for multiple contexts at once by specifying the
contexts separated by spaces in the name attribute.

- **Frame**
    - The entire window frame for any window (except the desktop).
      This includes both the window decorations (if any) and the application
      window itself.
        - **Note:** When a button is bound in this context, the clicks will
          *not* be passed through to the application. Use with care.
- **Client**
    - The application window, inside the window decorations.
        - **Note**: When a button is bound in this context, the clicks
          *will* be passed through to the application. However, because of
          this, only "Press" events can be used for this context.
- **Desktop**
    - The desktop, or background, regardless of if you use a program to
      place icons on your desktop or not (such as in KDE and GNOME). This
      is also called the "root window" frequently.
- **Root**
    - This works similarly to the Desktop context. However, this is a
      special context for bindings you only want to work only when you
      *don't* have a program running to place icons on your desktop.
      Generally this is only used for the root menus, so that they won't
      override the menus provided by your desktop icons.
- **Titlebar**
    - The decorations on the top of each application window
- **Top**, **Bottom**, **Left**, **Right**
    - The top, bottom, left or right edge of a window
- **TLCorner**, **TRCorner**, **BLCorner**, **BRCorner**
    - The top-left, top-right, bottom-left or bottom-right corner of a window
- **Icon**
    - The window icon shown in window titlebars
- **Iconify**
    - The iconify button shown in window titlebars
- **Maximize**
    - The maximize button shown in window titlebars
- **Close**
    - The close button shown in window titlebars
- **AllDesktops**
    - The all-desktops (omnipresent) button shown in window titlebars
- **Shade**
    - The shade button shown in window titlebars
- **MoveResize**
    - Bindings in this special context are available while a window is
      being moved or resized interactively

### Button

The **BUTTON** specifies which mouse button is used to trigger the mouse binding.

The named buttons are: `Left`, `Right`, `Middle`, `Up` (scroll wheel up)
and `Down` (scroll wheel down). To bind more than 5 buttons, use `Button6`,
`Button7` and so on.

You can also prefix the button name with a modifier as for key bindings
(see above section), for example `S-A-Down` for shift-alt-scroll wheel down.

You can create multiple mousebinds that trigger the same set of actions
by specifying them separated by spaces.

### Event

The **EVENT** for a mouse binding specifies what mouse event triggers
the actions contained within.

- **Press**
    - The mouse button was pressed down in the specified context
- **Click**
    - The mouse button was pressed and released in the specified context
- **DoubleClick**
    - The mouse button was double clicked in the specified context
- **Release**
    - The mouse button was released in the specified context
- **Drag**
    - The mouse was dragged with the mouse button held down in the
      specified context

### Actions

The **ACTIONS** can be any number of [actions](Actions.md).
They will generally be executed in order from the first to the last.
