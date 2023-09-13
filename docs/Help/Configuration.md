# Configuration

Openbox configuration is made essentially by modifying just one file called *rc.xml*.

Default configuration file can by default be found in `/etc/xdg/openbox/`
and a user specific file can be placed in `~/.config/openbox/`.

By default there is also `menu.xml` which is for menu configuration.
Menu configuration is separated from rest of the configs.

`rc.xml` is separated into different sections.
All the options are discussed below with examples.

## Resistance

```xml
<resistance>
  <strength>10</strength>
  <screen_edge_strength>20</screen_edge_strength>
</resistance>
```

**strength** Tells Openbox how much resistance (in pixels) there is
between two windows before it lets them overlap.

**screen_edge_strength** Basically the same as *strength* but between
window and the screen edge.

## Focus

```xml
<focus>
  <focusNew>yes</focusNew>
  <focusLast>yes</focusLast>
  <followMouse>no</followMouse>
  <focusDelay>200</focusDelay>
  <underMouse>no</underMouse>
  <raiseOnFocus>no</raiseOnFocus>
</focus>
```

**focusNew** Openbox will automatically give focus to new windows when
they are created, otherwise the focus will stay as it is.

**followMouse** Makes focus follow mouse. e.g. when the mouse is being
moved the focus will be given to window under the mouse cursor.

**focusLast** When switching desktops, focus the last focused window on
that desktop again, regardless of where the mouse is.
Only applies *followMouse* is set.

**focusDelay** The time (in milliseconds) Openbox will wait before
giving focus to the window under mouse cursor.
Only applies if *followMouse* is set.

**underMouse** Focus windows under the mouse not only when the mouse moves,
but also when it enters another window due to other reasons
(e.g. the window the mouse was in moved/closed/iconified etc).
Only applies if *followMouse* is set.

**raiseOnFocus** Also raises windows to top when they are focused. Only
applies if *followMouse* is set.

## Placement

```xml
<placement>
  <policy>Smart</policy>
  <center>no</center>
</placement>
```

**policy** can be either *Smart* or *UnderMouse*.

- *Smart* will cause new windows to be placed automatically by Openbox.
- *UnderMouse* makes new windows to be placed under the mouse cursor.

**center** can be either *yes* or *no*.
If it is enabled, windows will open centered in the free area found.

## Theme

```xml
<theme>
  <name>Clearlooks</name>
  <titleLayout>NLIMC</titleLayout>
  <keepBorder>yes</keepBorder>
  <animateIconify>yes</animateIconify>
  <font place="ActiveWindow">
    <name>sans</name>
    <size>8</size>
    <weight>bold</weight>
    <slant>normal</slant>
  </font>
  <font place="InactiveWindow">
    <name>sans</name>
    <size>8</size>
    <weight>bold</weight>
    <slant>normal</slant>
  </font>
  <font place="MenuHeader">
    <name>sans</name>
    <size>9</size>
    <weight>normal</weight>
    <slant>normal</slant>
  </font>
  <font place="MenuItem">
    <name>sans</name>
    <size>9</size>
    <weight>normal</weight>
    <slant>normal</slant>
  </font>
  <font place="OnScreenDisplay">
    <name>sans</name>
    <size>9</size>
    <weight>bold</weight>
    <slant>normal</slant>
  </font>
</theme>
```

**name** The name of the Openbox theme to use.

**titleLayout** tells in which order and what buttons should be in a window's titlebar.
The following letters can be used, each only once.

- N :window icon
- L :window label (aka. title)
- I: iconify
- M: maximize
- C: close
- S: shade (roll up/down)
- D: omnipresent (on all desktops).

![MSLDNI.png](../assets/img/MSLDNI.png)

![CLIM.png](../assets/img/CLIM.png)

**keepBorder** tells if windows should keep the border drawn by Openbox
when window decorations are turned off.

**animateIconify** adds a little iconification animation if enabled.
*font* Specifies the font to use for a specific element of the window.
Place can be either of:

- ActiveWindow: Title bar of the active window
- InactiveWindow: Title bar of the inactive window
- MenuHeader: Titles in the menu
- MenuItem: Items in the menu
- OnScreenDisplay: Text in popups such as window cycling or desktop switching popups

Childnodes for each place are name, specifying the font to use (defaults
to sans, an alias for all sans serif fonts), size in px, weight, either
normal or bold and slant, either italic or normal.

Themes themselves are described on the [theme specification](Themes.md) page.

## Desktops

```xml
<desktops>
  <number>4</number>
  <firstdesk>1</firstdesk>
  <popupTime>1000</popupTime>
  <names>
    <name>work</name>
    <name>play</name>
    <name>dull</name>
    <name>boy</name>
  </names>
</desktops>
```

**number** The number of virtual desktops to use.

**firstdesk** The number of the desktop to use when first started.

**popupTime** Time (in milliseconds) to show the popup when switching desktops.
Can be set to 0 to disable the popup completely.

**names** Each **name** tag names your desktops, in ascending order.
Unnamed desktops will be named automatically depending on the locale.
You can name more desktops than specified in *number* if you want.

## Resize (and move)

```xml
<resize>
  <drawContents>no</drawContents>
  <popupShow>Always</popupShow>
  <popupPosition>Fixed</popupPosition>
  <popupFixedposition>
    <x>400</x>
    <y>center</y>
  </popupFixedPosition>
</resize>
```

**drawContents** Resize the program inside the window while resizing.
When disabled the unused space will be filled with a uniform color during a resize.

**popupShow** When to show the move/resize popup. *Always* always shows it,
*Never* never shows it, *Nonpixel* shows it only when resizing windows that have
specified they are resized in increments larger than one pixel, usually terminals.

**popupPosition** Where to show the popup.

- *Top* shows the popup above the titlebar of the window.
- *Center* shows it centered on the window.
- *Fixed* shows it in a fixed location on the screen specified by *popupFixedPosition*.

**popupFixedPosition** Specifies where on the screen to show the position when *Fixed*.
Both *x* and *y* take coordinates as described [here](#coordinates).

## Applications

This section sets specific settings for applications, and is quite
complicated, so it has [its own page](Applications.md).

## Keyboard

```xml
<keyboard>
  <rebindOnMappingNotify>yes</rebindOnMappingNotify>
  <chainQuitKey>C-g</chainQuitKey>
  <keybind> ...
    ...
  </keybind>
</keyboard>
```

**rebindOnMappingNotify** If this is enabled, keybinds will be rebound
if the keyboard layout changes at runtime. It is enabled by default.
The rest of this section contains keyboard shortcuts and is described on
the [bindings page](Bindings.md#key-bindings).

## Mouse

```xml
<mouse>
  <dragThreshold>8</dragThreshold>
  <doubleClickTime>200</doubleClickTime>
  <screenEdgeWarpTime>400</screenEdgeWarpTime>
  <context> ...
    ...
  </context>
</mouse>
```

**dragThreshold** How many pixels you need to drag for it to be recognized
as a drag operation.

**doubleClickTime** Time (in milliseconds) allowed between two separate
clicks to register as a `DoubleClick`.

**screenEdgeWarpTime** Time (in milliseconds) to pause between two
consecutive desktop switches done by holding the cursor next to the
screen edge. Set to 0 to disable this feature.
The rest of this section contains mouse bindings and is described on the
[bindings page](Bindings.md#mouse-bindings).

## Margins

```xml
<margins>
  <top>50</top>
  <left>0</left>
  <right>20</right>
  <bottom>0</bottom>
</margins>
```

Each tag specifies the amount of pixels to reserve at the respective
edge of the screen. New windows will not be placed in those areas,
and maximized windows will not cover them.

## Menu

```xml
<menu>
  <hideDelay>250</hideDelay>
  <middle>no</middle>
  <submenuShowDelay>100</submenuShowDelay>
  <submenuHideDelay>400</submenuHideDelay>
  <applicationIcons>yes</applicationIcons>
  <manageDesktops>yes</manageDesktops>
  <file>menu.xml</file>
</menu>
```

**hideDelay** How long (in milliseconds) you have to hold the mouse
button down for it to be hidden automatically when you release it.
If you hold shorter, it will stay up when you release.

**middle** Position menus centered vertically instead of aligned to the top.

**submenuShowDelay** and **submenuHideDelay** affect how submenus pop up
when moving across them. When moving away from a submenu it is closed
after **submenuHideDelay**, and when moving into one, it is opened after
**submenuShowDelay**. When moving from one submenu to another, the hide
delay is only used if it is lower than the show delay (e.g. by default
it is not used). The old submenu is closed after *HideDelay*
milliseconds, and after *ShowDelay* milliseconds (after moving) the new
one is shown (and the old one is hidden even if *HideDelay* has not
expired yet).

**applicationIcons** Whether to show window icons in the Desktop
and Windows menus (client-list-menu and client-list-combined-menu).

**manageDesktops** Whether to show the *Add new desktop* and *Remove
last desktop* entries in the Desktop and Windows menus.

**file** Specify files to load menu specifications from.
Can be given more than once, although care should be taken to avoid id clashes.
Files are searched for in the user directory first and then in the system directory.

## Dock

```xml
<dock>
  <position>TopLeft</position>
  <stacking>Normal</stacking>
  <direction>Vertical</direction>
  <floatingX>0</floatingX>
  <floatingY>0</floatingY>
  <autoHide>no</autoHide>
  <hideDelay>300</hideDelay>
  <showDelay>300</showDelay>
  <moveButton>Button8</moveButton>
  <noStrut>yes</noStrut>
</dock>
```

The dock is only shown when one or more
[dockapps](../FAQ.md#what-is-this-dock-i-hear-so-much-about)
are running.

**position** Specify where to show the dock. Can be one of *TopLeft*,
*Top*, *TopRight*, *Right*, *BottomRight*, *Bottom*, *BottomLeft*,
*Left* and *Floating*.

**stacking** Which window layer to put the dock in. Can be one of
*above*, *normal*, *below*. The dock can be raised and lowered by left
and middle clicking on it, among windows in the specified layer.

**direction** Specify if dockapps should be laid out in a *Vertical* or
*Horizontal* direction.

**floatingX** and **floatingY** When *position* is set to *Floating*,
these specify the pixel position of the dock. Cannot currently use the
slightly extended format described at the bottom of this page.

**autoHide** Whether to hide the dock automatically when the mouse is
not over it.

**hideDelay** and **showDelay** specify (in milleseconds) the delays for
hiding and showing the dock when the mouse leaves and enters it,
respectively.

**moveButton** Specifies which button to use for moving individual
dockapps around in the dock, see the [bindings page](Bindings.md#button) for details.

**noStrut** Specifies that the dock should not set a strut, which means
it won't stop windows from being placed or maximized over it. When
*position* is set to *Floating*, this is always on, since openbox
doesn't guess which edge it should belong to based on just the position.
You can use [margins](#margins) to emulate that if you want.

## Coordinates

Many places in openbox that take a coordinate supports a slightly
extended format. Most simply it can be just a number such as *300*. Such
a coordinate will be left- or top-aligned depending on which coordinate
it is. To align to the opposite edge, use *-300*. To specify a negative
offset, a *-* is also used, so you have to use *+-10* to offset 10
pixels negatively to the left/top and *--10* for the right/bottom edge.
Some things enforce being onscreen though, such as the move/resize popup.
