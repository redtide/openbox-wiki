# Themes

language: gb \| [fr](Themes_fr.md)

Openbox 3 themes are written as an X resource database, in a file named
`themerc`. The format is quite simple to learn, but there are an
enormous number of options available to you.

Each and every option has been documented, with details such as their
default values, and which values are or are not valid for them. But to
try make it a little more accessible, we'll start with an example theme,
which uses every possible option within it. Each of the options can be
clicked to read the details about it.

# Theme installation

Openbox themes are stored in one of the following places:

- System-wide themes are installed in `/usr/share/themes`.
- User-specific themes can be installed in `~/.local/share/themes` or in
  `~/.themes`.

# Theme selection

Choosing a theme to use is simple with the
[ObConf](../ObConf/About.md) tool. Alternatively, there are a number of
[Pipe menus](../Community/Pipemenus/index.md) which can perform this function for you.

If you wish to set the theme by hand, you need to edit the `<name>` key in
the `<theme>` section of your `rc.xml` file.
The [Configuration guide](Configuration.md) is a good place to start.

# Theme file structure

The file structure goes like this:

`ThemesDirectory  (such as /usr/share/themes)`
` |`
` +-> ThemeName  (This is the name of the theme, such as Clearlooks)`
`      |`
`      +-> openbox-3  (This the type of the theme - it's for Openbox 3!)`
`           |`
`           |-> themerc  (This is the main theme file, documented in this page)`
`           |`
`           |-> max.xbm  (These are optional xbm masks for the titlebar buttons)`
`           |-> close.xbm`
`           ...`
`           +-> shade.xbm`

![Important.png](../assets/img/Important.png)
[ObConf](../ObConf/About.md) can create a `.obt` Openbox Theme
Archive file out of a theme for distribution, and can also install
`.obt` files very easily.

# Example

This is not a real theme, and if you used it, there is no guarantee it
will look good in any way. It is just meant to show all of the options
and how they relate to eachother.

<code>

`# Window geometry`
[`padding.width`](#padding.width)`: 2`
[`padding.height`](#padding.height)`: 2`
[`border.width`](#border.width)`: 1`
[`window.client.padding.width`](#window.client.padding.width)`: 1`
[`window.client.padding.height`](#window.client.padding.height)`: 0`
[`window.handle.width`](#window.handle.width)`: 3`

`#Menu geometry`
[`menu.border.width`](#menu.border.width)`: 1`
[`menu.overlap.x`](#menu.overlap.x)`: 0`
[`menu.overlap.y`](#menu.overlap.y)`: 0`

`# Border colors`
[`window.active.border.color`](#window.active.border.color)`: #000000`
[`window.inactive.border.color`](#window.inactive.border.color)`: #000000`
[`menu.border.color`](#menu.border.color)`: #000000`
[`window.active.client.color`](#window.active.client.color)`: #ffffff`
[`window.inactive.client.color`](#window.inactive.client.color)`: #cccccc`

`# Text shadows`
[`window.active.label.text.font`](#window.active.label.text.font)`: shadow=y:shadowtint=70:shadowoffset=1`
[`window.inactive.label.text.font`](#window.inactive.label.text.font)`: shadow=y:shadowtint=20:shadowoffset=1`
[`menu.items.font`](#menu.items.font)`: shadow=n`
[`menu.title.text.font`](#menu.title.text.font)`: shadow=y:shadowtint=70:shadowoffset=1`

`# Window title justification`
[`window.label.text.justify`](#window.label.text.justify)`: Center`

`# Active window`
[`window.active.title.bg`](#window.active.title.bg)`: Raised Gradient Vertical Interlaced`
[`window.active.title.bg`](#window.active.title.bg)`.color: #658fb5`
[`window.active.title.bg`](#window.active.title.bg)`.colorTo: #4d6982`
[`window.active.title.bg`](#window.active.title.bg)`.interlace.color: #7788cc`

[`window.active.label.bg`](#window.active.label.bg)`: Parentrelative`
[`window.active.label.text.color`](#window.active.label.text.color)`: #ffffff`

[`window.active.handle.bg`](#window.active.handle.bg)`: Raised Gradient Vertical`
[`window.active.handle.bg`](#window.active.handle.bg)`.color: #658fb5`
[`window.active.handle.bg`](#window.active.handle.bg)`.colorTo: #4d6982`

[`window.active.grip.bg`](#window.active.grip.bg)`: Raised Gradient Vertical`
[`window.active.grip.bg`](#window.active.grip.bg)`.color: #658fb5`
[`window.active.grip.bg`](#window.active.grip.bg)`.colorTo: #4d6982`

[`window.active.button.unpressed.bg`](#window.active.button.unpressed.bg)`: Flat Gradient Vertical Border`
[`window.active.button.unpressed.bg`](#window.active.button.unpressed.bg)`.color: #6993b9`
[`window.active.button.unpressed.bg`](#window.active.button.unpressed.bg)`.colorTo: #55799a`
[`window.active.button.unpressed.bg`](#window.active.button.unpressed.bg)`.border.color: #3d4c5a`
[`window.active.button.unpressed.image.color`](#window.active.button.unpressed.image.color)`: #ffffff`

[`window.active.button.pressed.bg`](#window.active.button.pressed.bg)`: Flat Gradient Vertical Border`
[`window.active.button.pressed.bg`](#window.active.button.pressed.bg)`.color: #537797`
[`window.active.button.pressed.bg`](#window.active.button.pressed.bg)`.colorTo: #50708e`
[`window.active.button.pressed.bg`](#window.active.button.pressed.bg)`.border.color: #3d4c5a`
[`window.active.button.pressed.image.color`](#window.active.button.pressed.image.color)`: #ffffff`

[`window.active.button.disabled.bg`](#window.active.button.disabled.bg)`: Flat Gradient Vertical Border`
[`window.active.button.disabled.bg`](#window.active.button.disabled.bg)`.color: #537797`
[`window.active.button.disabled.bg`](#window.active.button.disabled.bg)`.colorTo: #50708e`
[`window.active.button.disabled.bg`](#window.active.button.disabled.bg)`.border.color: #3d4c5a`
[`window.active.button.disabled.image.color`](#window.active.button.disabled.image.color)`: #3d4c5a`

[`window.active.button.hover.bg`](#window.active.button.hover.bg)`: Flat Gradient Vertical Border`
[`window.active.button.hover.bg`](#window.active.button.hover.bg)`.color: #6993b9`
[`window.active.button.hover.bg`](#window.active.button.hover.bg)`.colorTo: #55799a`
[`window.active.button.hover.bg`](#window.active.button.hover.bg)`.border.color: #3d4c5a`
[`window.active.button.hover.image.color`](#window.active.button.hover.image.color)`: #ffffff`

[`window.active.button.toggled.unpressed.bg`](#window.active.button.toggled.unpressed.bg)`: Flat Gradient Vertical Border`
[`window.active.button.toggled.unpressed.bg`](#window.active.button.toggled.unpressed.bg)`.color: #6993b9`
[`window.active.button.toggled.unpressed.bg`](#window.active.button.toggled.unpressed.bg)`.colorTo: #55799a`
[`window.active.button.toggled.unpressed.bg`](#window.active.button.toggled.unpressed.bg)`.border.color: #3d4c5a`
[`window.active.button.toggled.unpressed.image.color`](#window.active.button.toggled.unpressed.image.color)`: #cccccc`

[`window.active.button.toggled.pressed.bg`](#window.active.button.toggled.pressed.bg)`: Flat Gradient Vertical Border`
[`window.active.button.toggled.pressed.bg`](#window.active.button.toggled.pressed.bg)`.color: #537797`
[`window.active.button.toggled.pressed.bg`](#window.active.button.toggled.pressed.bg)`.colorTo: #50708e`
[`window.active.button.toggled.pressed.bg`](#window.active.button.toggled.pressed.bg)`.border.color: #3d4c5a`
[`window.active.button.toggled.pressed.image.color`](#window.active.button.toggled.pressed.image.color)`: #ffffff`

[`window.active.button.toggled.hover.bg`](#window.active.button.toggled.hover.bg)`: Flat Gradient Vertical Border`
[`window.active.button.toggled.hover.bg`](#window.active.button.toggled.hover.bg)`.color: #6993b9`
[`window.active.button.toggled.hover.bg`](#window.active.button.toggled.hover.bg)`.colorTo: #55799a`
[`window.active.button.toggled.hover.bg`](#window.active.button.toggled.hover.bg)`.border.color: #3d4c5a`
[`window.active.button.toggled.hover.image.color`](#window.active.button.toggled.hover.image.color)`: #ffffff`

`# Inactive windows`
[`window.inactive.title.bg`](#window.inactive.title.bg)`: Raised Gradient Vertical`
[`window.inactive.title.bg`](#window.inactive.title.bg)`.color: #f1eeea`
[`window.inactive.title.bg`](#window.inactive.title.bg)`.colorTo: #d8cfc7`

[`window.inactive.label.bg`](#window.inactive.label.bg)`: Parentrelative`
[`window.inactive.label.text.color`](#window.inactive.label.text.color)`: #000000`

[`window.inactive.handle.bg`](#window.inactive.handle.bg)`: Raised Gradient Vertical`
[`window.inactive.handle.bg`](#window.inactive.handle.bg)`.color: #f1eeea`
[`window.inactive.handle.bg`](#window.inactive.handle.bg)`.colorTo: #d8cfc7`

[`window.inactive.grip.bg`](#window.inactive.grip.bg)`: Raised Gradient Vertical`
[`window.inactive.grip.bg`](#window.inactive.grip.bg)`.color: #f1eeea`
[`window.inactive.grip.bg`](#window.inactive.grip.bg)`.colorTo: #d8cfc7`

[`window.inactive.button.unpressed.bg`](#window.inactive.button.unpressed.bg)`: Flat Gradient Vertical Border`
[`window.inactive.button.unpressed.bg`](#window.inactive.button.unpressed.bg)`.color: #efebe7`
[`window.inactive.button.unpressed.bg`](#window.inactive.button.unpressed.bg)`.colorTo: #ddd6ce`
[`window.inactive.button.unpressed.bg`](#window.inactive.button.unpressed.bg)`.border.color: #8f8173`
[`window.inactive.button.unpressed.image.color`](#window.inactive.button.unpressed.image.color)`: #000000`

[`window.inactive.button.pressed.bg`](#window.inactive.button.pressed.bg)`: Flat Gradient Vertical Border`
[`window.inactive.button.pressed.bg`](#window.inactive.button.pressed.bg)`.color: #efebe7`
[`window.inactive.button.pressed.bg`](#window.inactive.button.pressed.bg)`.colorTo: #ddd6ce`
[`window.inactive.button.pressed.bg`](#window.inactive.button.pressed.bg)`.border.color: #8f8173`
[`window.inactive.button.pressed.image.color`](#window.inactive.button.pressed.image.color)`: #000000`

[`window.inactive.button.disabled.bg`](#window.inactive.button.disabled.bg)`: Flat Gradient Vertical Border`
[`window.inactive.button.disabled.bg`](#window.inactive.button.disabled.bg)`.color: #efebe7`
[`window.inactive.button.disabled.bg`](#window.inactive.button.disabled.bg)`.colorTo: #ddd6ce`
[`window.inactive.button.disabled.bg`](#window.inactive.button.disabled.bg)`.border.color: #8f8173`
[`window.inactive.button.disabled.image.color`](#window.inactive.button.disabled.image.color)`: #8f8173`

[`window.inactive.button.toggled.bg`](#window.inactive.button.toggled.bg)`: Flat Gradient Vertical Border`
[`window.inactive.button.toggled.bg`](#window.inactive.button.toggled.bg)`.color: #efebe7`
[`window.inactive.button.toggled.bg`](#window.inactive.button.toggled.bg)`.colorTo: #ddd6ce`
[`window.inactive.button.toggled.bg`](#window.inactive.button.toggled.bg)`.border.color: #8f8173`
[`window.inactive.button.toggled.image.color`](#window.inactive.button.toggled.image.color)`: #000000`

[`window.inactive.button.hover.bg`](#window.inactive.button.hover.bg)`: Flat Gradient Vertical Border`
[`window.inactive.button.hover.bg`](#window.inactive.button.hover.bg)`.color: #efebe7`
[`window.inactive.button.hover.bg`](#window.inactive.button.hover.bg)`.colorTo: #ddd6ce`
[`window.inactive.button.hover.bg`](#window.inactive.button.hover.bg)`.border.color: #8f8173`
[`window.inactive.button.hover.image.color`](#window.inactive.button.hover.image.color)`: #000000`

[`window.inactive.button.toggled.unpressed.bg`](#window.inactive.button.toggled.unpressed.bg)`: Flat Gradient Vertical Border`
[`window.inactive.button.toggled.unpressed.bg`](#window.inactive.button.toggled.unpressed.bg)`.color: #efebe7`
[`window.inactive.button.toggled.unpressed.bg`](#window.inactive.button.toggled.unpressed.bg)`.colorTo: #ddd6ce`
[`window.inactive.button.toggled.unpressed.bg`](#window.inactive.button.toggled.unpressed.bg)`.border.color: #8f8173`
[`window.inactive.button.toggled.unpressed.image.color`](#window.inactive.button.toggled.unpressed.image.color)`: #000000`

[`window.inactive.button.toggled.pressed.bg`](#window.inactive.button.toggled.pressed.bg)`: Flat Gradient Vertical Border`
[`window.inactive.button.toggled.pressed.bg`](#window.inactive.button.toggled.pressed.bg)`.color: #efebe7`
[`window.inactive.button.toggled.pressed.bg`](#window.inactive.button.toggled.pressed.bg)`.colorTo: #ddd6ce`
[`window.inactive.button.toggled.pressed.bg`](#window.inactive.button.toggled.pressed.bg)`.border.color: #8f8173`
[`window.inactive.button.pressed.toggled.image.color`](#window.inactive.button.toggled.pressed.image.color)`: #000000`

[`window.inactive.button.toggled.hover.bg`](#window.inactive.button.toggled.hover.bg)`: Flat Gradient Vertical Border`
[`window.inactive.button.toggled.hover.bg`](#window.inactive.button.toggled.hover.bg)`.color: #efebe7`
[`window.inactive.button.toggled.hover.bg`](#window.inactive.button.toggled.hover.bg)`.colorTo: #ddd6ce`
[`window.inactive.button.toggled.hover.bg`](#window.inactive.button.toggled.hover.bg)`.border.color: #8f8173`
[`window.inactive.button.toggled.hover.image.color`](#window.inactive.button.toggled.hover.image.color)`: #000000`

`# Menus`
[`menu.title.bg`](#menu.title.bg)`: Raised Gradient Vertical`
[`menu.title.bg`](#menu.title.bg)`.color: #658fb5`
[`menu.title.bg`](#menu.title.bg)`.colorTo: #4d6982`
[`menu.title.text.color`](#menu.title.text.color)`: #ffffff`
[`menu.title.text.justify`](#menu.title.text.justify)`: Left`

[`menu.separator.color`](#menu.separator.color)`: #444444`
[`menu.separator.width`](#menu.separator.width)`: 1`
[`menu.separator.padding.width`](#menu.separator.padding.width)`: 6`
[`menu.separator.padding.height`](#menu.separator.padding.height)`: 3`

[`menu.items.bg`](#menu.items.bg)`: Flat Solid`
[`menu.items.bg`](#menu.items.bg)`.color: #f8f5f2`
[`menu.items.text.color`](#menu.items.text.color)`: #000000`
[`menu.items.disabled.text.color`](#menu.items.disabled.text.color)`: #aaaaaa`

[`menu.items.active.bg`](#menu.items.active.bg)`: Flat Gradient Vertical`
[`menu.items.active.bg`](#menu.items.active.bg)`.color: #628cb2`
[`menu.items.active.bg`](#menu.items.active.bg)`.colorTo: #50708d`
[`menu.items.active.text.color`](#menu.items.active.text.color)`: #ffffff`
[`menu.items.active.disabled.text.color`](#menu.items.active.disabled.text.color)`: #aaaaaa`

</code>

# Data types

## Integers

These are simply numbers like `1` or `42`. They can be prime, composite,
or zero.

Example: <code>

    window.handle.width: 3

</code>

## Justification

These determines how to justify text. Valid options are `Left`, `Center`
and `Right`.

Example: <code>

    menu.title.text.justify: Left

</code>

## Textures

These determine the visual look of an element. They are the most
complicated part of a theme file, but they are still not too tricky.

Textures are specified through a text string with a number of fields.
Capitalization is not significant. The format is as follows (`|` stands
for "or" and `[]` surround optional fields):

    parentrelative | ((solid | gradient gradient-type) [border] [interlaced])

We'll dissect what that means exactly.

### Parentrelative

Parentrelative means that the element inherits its colors from the
textures behind it. It is, in essence, completely transparent . Some
theme elements can be parentrelative, and some can not. The
documentation for each one will tell you if you can use parentrelative
for it or not.

Example: <code>

    window.active.label.bg: Parentrelative
    window.inactive.label.bg: Parentrelative Raised

</code>

### Solid

Solid means that the background of the texture is filled with a single
color. The texture *must* be accompanied by a single [color
field](#Colors).

Example: <code>

    menu.items.bg:       Solid Flat
    menu.items.bg.color: #f8f5f2

</code>

### Gradients

When a gradient is specified, it must be followed by the gradient's
type. Gradients all use two [color fields](#Colors): `color`
and `colorTo` and must also be accompanied by these.

Valid gradient types are:

- Diagonal - A gradient from the top left corner to the bottom right
  corner
- CrossDiagonal - A gradient from the top right corner to the bottom
  left corner
- Pyramid - A gradient that starts in all four corners and smooths to
  the center of the texture
- Horizontal - A gradient from the left edge to the right
- MirrorHorizontal - A gradient from the left edge to the middle, and
  then reversed to the right edge
- Vertical - A gradient from the top edge to the bottom
- SplitVertical - A gradient split in the middle that goes out toward
  the top and bottom edges

Example: <code>

    menu.title.bg:         Gradient Vertical Raised
    menu.title.bg.color:   #658fb5
    menu.title.bg.colorTo: #4d6982

</code>

#### SplitVertical gradients

SplitVertical gradients have 2 optional, addition [color
fields](#Colors): `color.splitTo` and `colorTo.splitTo`.
These colors are the light colors used on the far top and bottom of the
SplitVertical gradient. When these are omitted, then the default values
for these are `color` \* 5/4, and `colorTo` \* 17/16.

Example: <code>

    menu.title.bg:                 Gradient SplitVertical Raised
    menu.title.bg.color:           #658fb5
    menu.title.bg.color.splitTo:   #7595b9
    menu.title.bg.colorTo:         #4d6982
    menu.title.bg.colorTo.splitTo: #557485

</code>

### Border

Borders can be used on both solid and gradient textures. Valid options
for the border are `Flat`, `Raised` and `Sunken`. When a border is not
specified, `Raised` is assumed.

Flat, by default, means no border at all. To add a flat solid border,
use `Flat Border`. When using a flat border, the texture *must* be
accompanied by a [border color](#Colors).

Example: <code>

    window.active.button.unpressed.bg:              Gradient Vertical Flat Border
    window.active.button.unpressed.bg.border.color: #3d4c5a

</code>

Raised and Sunken have two bevel options available to them. By default,
a bevel is drawn around the very outside of the texture. If `Bevel2` is
specified, then the bevel is drawn slightly in from the edge. This can
be used to animate button presses/toggled states.

The strength of the bevel highlights can also be determined by the
theme, by using the `highlight` and `shadow` fields:

The `highlight` field specifies the strength of the light bevel. It is a
value above or equal to 0, where 0 makes no highlight at all, 256 makes
the highlight color 100% brighter, 512 makes the highlight color 200%
brighter, and so on. The default `highlight` is 128 (which is a 50%
increase in brightness).

The `shadow` field specifies the strength of the dark bevel. It is a
value between 0 and 256, where 0 makes no shadow at all, and 256 makes a
completely black shadow (100% decreased brightness). The default
`shadow` is 64 (which is a 25% decrease in brightness).

Example: <code>

    window.inactive.button.disabled.bg:           Gradient Diagonal Raised
    window.inactive.button.disabled.bg.color:     rgb:50/54/58
    window.inactive.button.disabled.bg.colorTo:   black
    window.inactive.button.disabled.bg.highlight: 128
    window.inactive.button.disabled.bg.shadow:    64

    window.inactive.button.toggled.pressed.bg:          Gradient Diagonal Raised Bevel2
    window.inactive.button.toggled.pressed.bg.color:    rgb:50/54/58
    window.inactive.button.toggled.pressed.bg.colorTo:  black

</code>

### Interlaced

Interlaced textures have a solid line drawn horizontally every second
row. When you specify `interlaced`, the texture *must* be accompanied by
an [interlaced color](#Colors).

Example: <code>

    window.inactive.title.bg: Solid Flat Interlaced
    window.inactive.title.bg.color: #f5f5f5
    window.inactive.title.bg.interlace.color: #f6f6f6

</code>

## Colors

Colors can be specified by name or by their hexadecimal RGB value.

### Color names

Wikipedia has a [list of X11 color
names](http://en.wikipedia.org/wiki/Web_colors#X11_color_names), and
further [details here](http://en.wikipedia.org/wiki/X11_color_names).

Example: <code>

    menu.items.active.text.color: white
    window.active.grip.bg.color: grey40

</code>

### RGB values

Colors can be specified by hexadecimal RGB values in two ways. The most
familiar is through syntax similar to HTML, `#rrggbb`. However you may
also use the format `rgb:rr/bb/gg`. What goes inside them for the `rr`,
`gg` and `bb` values is identical.

Example: <code>

    window.active.grip.bg.color: #658fb5
    window.active.label.text.color: #fff
    menu.items.active.bg.color: rgb:90/94/98
    window.active.title.bg.color: rgb:6/9/c

</code>

Note that `#fff` is equivalent to `#f0f0f0`, *not* to `#ffffff`.

## Text shadow strings

Text shadows are specified through a specially formatted text string.

There are three properties that can be placed in the string: `shadow`,
`shadowtint` and `shadowoffset`.

Shadow is a boolean value. It defaults to no. You can enable a shadow
for text by using `shadow=y`.

Shadowtint specifies the alpha value for the shadow as well as its color
(black or white). It defaults to black and 50% opacity. You can specify
the shadowtint by using `shadowtint=70`. The tint can be any integer
between -100 and 100. 0 means 0% opacity (invisible), 100 means 100%
opacity and black, -100 means 100% opacity and white.

Shadowoffset specifies how far the shadow is should be offset from the
text. It defaults to 1. It can be positive to move the shadow and and
right from the text, or negative to move it up and left from the text.
You can set the shadowoffset by using `shadowoffset=2`. A shadowoffset
of 0 will place it exactly behind the text and it will not be visible.

The text shadow string used to be for choosing a font for the theme as
well. Any other properties in the string, such as those for choosing a
font, are ignored.

Example: <code>

    window.active.label.text.font:shadow=y:shadowtint=70:shadowoffset=1

</code>

# Theme elements

Each theme element corresponds to one part of a window or a menu. We'll
start be discussing the elements that let you change the size and
placement of things, and then talk about how to change the textures used
to render everything.

We're going to use a table such as this to describe each element:

| Type:           | [integer](#Integers) |
|-----------------|---------------------------------|
| Default:        | 1                               |
| Valid:          | 0-100                           |
| Parentrelative: | no                              |

Type shows the type of the value for the element.

Default gives the default value for the element if it is not listed in
the theme. When Default refers to another theme element, then it means
that element's values are used.

Valid gives valid ranges for elements that this is applicable for, such
as [integer values](#Integers).

Parentrelative specifies if a given texture may use the
[Parentrelative](#Parentrelative) visual type, when
applicable.

## Geometry

### border.width

| Type:    | [integer](#Integers) |
|----------|---------------------------------|
| Default: | 1                               |
| Valid:   | 0 - 100                         |

Specifies the size of the border drawn around window frames.

See also:
[window.active.border.color](#window.active.border.color),
[window.inactive.border.color](#window.inactive.border.color)

### menu.border.width

| Type:    | [integer](#Integers)          |
|----------|------------------------------------------|
| Default: | [border.width](#border.width) |
| Valid:   | 0 - 100                                  |

Specifies the size of the border drawn around menus.

See also: [menu.border.color](#menu.border.color)

### menu.separator.width

| Type:    | [integer](#Integers) |
|----------|---------------------------------|
| Default: | 1                               |
| Valid:   | 1 - 100                         |

Specifies the size of menu line separators.
<span style="color:green">***(As of version 3.4.7)***</span>

### menu.separator.padding.width

| Type:    | [integer](#Integers) |
|----------|---------------------------------|
| Default: | 6                               |
| Valid:   | 0 - 100                         |

Specifies the space on the left and right side of menu line separators.
<span style="color:green">***(As of version 3.4.7)***</span>

See also:
[menu.separator.padding.height](#menu.separator.padding.height)

### menu.separator.padding.height

| Type:    | [integer](#Integers) |
|----------|---------------------------------|
| Default: | 3                               |
| Valid:   | 0 - 100                         |

Specifies the space on the top and bottom of menu line separators.
<span style="color:green">***(As of version 3.4.7)***</span>

See also:
[menu.separator.padding.width](#menu.separator.padding.width)

### osd.border.width

| Type:    | [integer](#Integers)          |
|----------|------------------------------------------|
| Default: | [border.width](#border.width) |
| Valid:   | 0 - 100                                  |

Specifies the size of the border drawn on-screen-dialogs, such as the
focus cycling (Alt-Tab) dialog.

See also: [osd.border.color](#osd.border.color)

### window.client.padding.width

| Type:    | [integer](#Integers)            |
|----------|--------------------------------------------|
| Default: | [padding.width](#padding.width) |
| Valid:   | 0 - 100                                    |

Specifies the size of the left and right sides of the inner border. The
inner border is drawn around the window, but inside the other
decorations.

See also:
[window.active.client.color](#window.active.client.color),
[window.inactive.client.color](#window.inactive.client.color)
[window.client.padding.height](#window.client.padding.height)

### window.client.padding.height

| Type:    | [integer](#Integers)                                        |
|----------|------------------------------------------------------------------------|
| Default: | [window.client.padding.width](#window.client.padding.width) |
| Valid:   | 0 - 100                                                                |

Specifies the size of the top and bottom sides of the inner border. The
inner border is drawn around the window, but inside the other
decorations.

See also:
[window.active.client.color](#window.active.client.color),
[window.inactive.client.color](#window.inactive.client.color)
[window.client.padding.width](#window.client.padding.width)

### window.handle.width

| Type:    | [integer](#Integers) |
|----------|---------------------------------|
| Default: | 6                               |
| Valid:   | 0 - 100                         |

Specifies the size of the window handle. The window handle is the piece
of decorations on the bottom of windows. A value of 0 means that no
handle is shown.

See also:
[window.active.handle.bg](#window.active.handle.bg),
[window.inactive.handle.bg](#window.inactive.handle.bg),
[window.active.grip.bg](#window.active.grip.bg),
[window.inactive.grip.bg](#window.inactive.grip.bg)

### padding.width

| Type:    | [integer](#Integers) |
|----------|---------------------------------|
| Default: | 3                               |
| Valid:   | 0 - 100                         |

Specifies the padding size, used for spacing out elements in the window
decorations. This can be used to give a theme a more compact or a more
relaxed feel. This specifies padding in the horizontal direction (and
vertical direction if [padding.height](#padding.height) is
not explicitly set).

See also: [padding.height](#padding.height)

### padding.height

| Type:    | [integer](#Integers)            |
|----------|--------------------------------------------|
| Default: | [padding.width](#padding.width) |
| Valid:   | 0 - 100                                    |

Specifies the padding size, used for spacing out elements in the window
decorations. This can be used to give a theme a more compact or a more
relaxed feel. This specifies padding in only the vertical direction.

See also: [padding.width](#padding.width)

### menu.overlap.x

| Type:    | [integer](#Integers)          |
|----------|------------------------------------------|
| Default: | [menu.overlap](#menu.overlap) |
| Valid:   | -100 - 100                               |

Specifies how sub menus should overlap their parents. A positive value
moves the submenu over top of their parent by that amount. A negative
value moves the submenu away from their parent by that amount.
<span style="color:green">***(As of version 3.4.7)***</span>

See also: [menu.overlap.y](#menu.overlap.y)

### menu.overlap.y

| Type:    | [integer](#Integers)          |
|----------|------------------------------------------|
| Default: | [menu.overlap](#menu.overlap) |
| Valid:   | -100 - 100                               |

Specifies how sub menus should be positioned relative to their parents.
A positive value moves the submenu vertically down by that amount, a
negative value moves it up by that amount.
<span style="color:green">***(As of version 3.4.7)***</span>

See also: [menu.overlap.x](#menu.overlap.x)

### menu.overlap

| Type:    | [integer](#Integers) |
|----------|---------------------------------|
| Default: | 0                               |
| Valid:   | -100 - 100                      |

<span style="color:red">***This property is obsolete and only present
for backwards compatibility.***</span>

See also: [menu.overlap.x](#menu.overlap.x),
[menu.overlap.y](#menu.overlap.y)

## Border colors

### window.active.border.color

| Type:    | [color](#Colors)              |
|----------|------------------------------------------|
| Default: | [border.color](#border.color) |

Specifies the border color for the focused window.

See also: [border.width](#border.width),
[window.inactive.border.color](#window.inactive.border.color)

### window.active.title.separator.color

| Type:    | [color](#Colors)                                          |
|----------|----------------------------------------------------------------------|
| Default: | [window.active.border.color](#window.active.border.color) |

Specifies the border color for the border between the titlebar and the
window, for the focused window.

See also:
[window.inactive.title.separator.color](#window.inactive.title.separator.color)

### window.inactive.border.color

| Type:    | [color](#Colors)                                          |
|----------|----------------------------------------------------------------------|
| Default: | [window.active.border.color](#window.active.border.color) |

Specifies the border color for all non-focused windows.

See also: [border.width](#border.width),
[window.active.border.color](#window.active.border.color)

### window.inactive.title.separator.color

| Type:    | [color](#Colors)                                              |
|----------|--------------------------------------------------------------------------|
| Default: | [window.inactive.border.color](#window.inactive.border.color) |

Specifies the border color for the border between the titlebar and the
window, for non-focused windows.

See also:
[window.active.title.separator.color](#window.active.title.separator.color)

### border.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

<span style="color:red">***This property is obsolete and only present
for backwards compatibility.***</span>

See also:
[window.active.border.color](#window.active.border.color),
[window.inactive.border.color](#window.inactive.border.color),
[menu.border.color](#menu.border.color)

### window.active.client.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | white                       |

Specifies the color of the inner border for the focused window, drawn
around the window but inside the other decorations.

See also:
[window.client.padding.width](#window.client.padding.width),
[window.inactive.client.color](#window.inactive.client.color)

### window.inactive.client.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | white                       |

Specifies the color of the inner border for non-focused windows, drawn
around the window but inside the other decorations.

See also:
[window.client.padding.width](#window.client.padding.width),
[window.active.client.color](#window.active.client.color)

### menu.border.color

| Type:    | [color](#Colors)                                          |
|----------|----------------------------------------------------------------------|
| Default: | [window.active.border.color](#window.active.border.color) |

Specifies the border color for menus.

See also: [menu.border.width](#menu.border.width)

### osd.border.color

| Type:    | [color](#Colors)                                          |
|----------|----------------------------------------------------------------------|
| Default: | [window.active.border.color](#window.active.border.color) |

Specifies the border color for on-screen-dialogs, such as the focus
cycling (Alt-Tab) dialog.

See also: [osd.border.width](#osd.border.width)

## Titlebar colors

### window.active.label.text.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

Specifies the color of the titlebar text for the focused window.

See also:
[window.inactive.label.text.color](#window.inactive.label.text.color)

### window.inactive.label.text.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | white                       |

Specifies the color of the titlebar text for non-focused windows.

See also:
[window.active.label.text.color](#window.active.label.text.color)

### window.active.button.unpressed.image.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

Specifies the color of the images in titlebar buttons in their default,
unpressed, state. This element is for the focused window.

See also:
[window.inactive.button.unpressed.image.color](#window.inactive.button.unpressed.image.color)

### window.active.button.pressed.image.color

| Type:    | [color](#Colors)                                                                          |
|----------|------------------------------------------------------------------------------------------------------|
| Default: | [window.active.button.unpressed.image.color](#window.active.button.unpressed.image.color) |

Specifies the color of the images in titlebar buttons when they are
being pressed by the user. This element is for the focused window.

See also:
[window.inactive.button.pressed.image.color](#window.inactive.button.pressed.image.color)

### window.active.button.disabled.image.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | white                       |

Specifies the color of the images in titlebar buttons when they are
disabled for the window. This element is for the focused window.

See also:
[window.inactive.button.disabled.image.color](#window.inactive.button.disabled.image.color)

### window.active.button.hover.image.color

| Type:    | [color](#Colors)                                                                          |
|----------|------------------------------------------------------------------------------------------------------|
| Default: | [window.active.button.unpressed.image.color](#window.active.button.unpressed.image.color) |

Specifies the color of the images in titlebar buttons when the mouse is
over top of the button. This element is for the focused window.

See also:
[window.inactive.button.hover.image.color](#window.inactive.button.hover.image.color)

### window.active.button.toggled.unpressed.image.color

| Type:    | [color](#Colors)                                                                      |
|----------|--------------------------------------------------------------------------------------------------|
| Default: | [window.active.button.toggled.image.color](#window.active.button.toggled.image.color) |

Specifies the color of the images in titlebar buttons when the button is
toggled - such as when a window is maximized. This element is for the
focused window.

See also:
[window.inactive.button.toggled.unpressed.image.color](#window.inactive.button.toggled.unpressed.image.color)

### window.active.button.toggled.pressed.image.color

| Type:    | [color](#Colors)                                                                      |
|----------|--------------------------------------------------------------------------------------------------|
| Default: | [window.active.button.pressed.image.color](#window.active.button.pressed.image.color) |

Specifies the color of the images in the titlebar buttons if they are
pressed on with the mouse while they are in the toggled state - such as
when a window is maximized. This element is for the focused window.

See also:
[window.inactive.button.toggled.pressed.image.color](#window.inactive.button.toggled.pressed.image.color)

### window.active.button.toggled.hover.image.color

| Type:    | [color](#Colors)                                                                                          |
|----------|----------------------------------------------------------------------------------------------------------------------|
| Default: | [window.active.button.toggled.unpressed.image.color](#window.active.button.toggled.unpressed.image.color) |

Specifies the color of the images in the titlebar buttons when the mouse
is hovered over them while they are in the toggled state - such as when
a window is maximized. This element is for the focused window.

See also:
[window.inactive.button.toggled.hover.image.color](#window.inactive.button.toggled.hover.image.color)

### window.active.button.toggled.image.color

| Type:    | [color](#Colors)                                                                      |
|----------|--------------------------------------------------------------------------------------------------|
| Default: | [window.active.button.pressed.image.color](#window.active.button.pressed.image.color) |

<span style="color:red">***This property is obsolete and only present
for backwards compatibility.***</span>

### window.inactive.button.unpressed.image.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | white                       |

Specifies the color of the images in titlebar buttons in their default,
unpressed, state. This element is for non-focused windows.

See also:
[window.active.button.unpressed.image.color](#window.active.button.unpressed.image.color)

### window.inactive.button.pressed.image.color

| Type:    | [color](#Colors)                                                                              |
|----------|----------------------------------------------------------------------------------------------------------|
| Default: | [window.inactive.button.unpressed.image.color](#window.inactive.button.unpressed.image.color) |

Specifies the color of the images in titlebar buttons when they are
being pressed by the user. This element is for non-focused windows.

This color is also used for pressed color when the button is toggled.

See also:
[window.active.button.pressed.image.color](#window.active.button.pressed.image.color)

### window.inactive.button.disabled.image.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

Specifies the color of the images in titlebar buttons when they are
disabled for the window. This element is for non-focused windows.

See also:
[window.active.button.disabled.image.color](#window.active.button.disabled.image.color)

### window.inactive.button.hover.image.color

| Type:    | [color](#Colors)                                                                              |
|----------|----------------------------------------------------------------------------------------------------------|
| Default: | [window.inactive.button.unpressed.image.color](#window.inactive.button.unpressed.image.color) |

Specifies the color of the images in titlebar buttons when the mouse is
over top of the button. This element is for non-focused windows.

See also:
[window.active.button.hover.image.color](#window.active.button.hover.image.color)

### window.inactive.button.toggled.unpressed.image.color

| Type:    | [color](#Colors)                                                                          |
|----------|------------------------------------------------------------------------------------------------------|
| Default: | [window.inactive.button.toggled.image.color](#window.inactive.button.toggled.image.color) |

Specifies the color of the images in titlebar buttons when the button is
toggled - such as when a window is maximized. This element is for
non-focused windows.

See also:
[window.active.button.toggled.unpressed.image.color](#window.active.button.toggled.unpressed.image.color)

### window.inactive.button.toggled.pressed.image.color

| Type:    | [color](#Colors)                                                                          |
|----------|------------------------------------------------------------------------------------------------------|
| Default: | [window.inactive.button.pressed.image.color](#window.inactive.button.pressed.image.color) |

Specifies the color of the images in the titlebar buttons if they are
pressed on with the mouse while they are in the toggled state - such as
when a window is maximized. This element is for non-focused windows.

See also:
[window.active.button.toggled.pressed.image.color](#window.active.button.toggled.pressed.image.color)

### window.inactive.button.toggled.hover.image.color

| Type:    | [color](#Colors)                                                                                              |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| Default: | [window.inactive.button.toggled.unpressed.image.color](#window.inactive.button.toggled.unpressed.image.color) |

Specifies the color of the images in the titlebar buttons when the mouse
is hovered over them while they are in the toggled state - such as when
a window is maximized. This element is for non-focused windows.

See also:
[window.active.button.toggled.hover.image.color](#window.active.button.toggled.hover.image.color)

### window.inactive.button.toggled.image.color

| Type:    | [color](#Colors)                                                                      |
|----------|--------------------------------------------------------------------------------------------------|
| Default: | [window.active.button.pressed.image.color](#window.active.button.pressed.image.color) |

<span style="color:red">***This property is obsolete and only present
for backwards compatibility.***</span>

## Active window textures

### window.active.title.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | no                              |

Specifies the background for the focused window's titlebar.

See also:
[window.inactive.title.bg](#window.inactive.title.bg)

### window.active.label.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

Specifies the background for the focused window's titlebar label. The
label is the container for the window title. When it is parentrelative,
then it uses the
[window.active.title.bg](#window.active.title.bg) which is
underneath it.

See also: [titlebar colors](#Titlebar_colors),
[window.inactive.label.bg](#window.inactive.label.bg),
[window.active.title.bg](#window.active.title.bg)

### window.active.handle.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | no                              |

Specifies the background for the focused window's handle. The handle is
the window decorations placed on the bottom of windows.

See also: [window.handle.width](#window.handle.width),
[window.inactive.handle.bg](#window.inactive.handle.bg)

### window.active.grip.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

Specifies the background for the focused window's grips. The grips are
located at the left and right sides of the window's handle. When it is
parentrelative, then it uses the
[window.active.handle.bg](#window.active.handle.bg) which is
underneath it.

See also: [window.handle.width](#window.handle.width),
[window.inactive.grip.bg](#window.inactive.grip.bg),
[window.active.handle.bg](#window.active.handle.bg)

## Inactive window textures

### window.inactive.title.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | no                              |

Specifies the background for non-focused windows' titlebars.

See also: [window.active.title.bg](#window.active.title.bg)

### window.inactive.label.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

Specifies the background for non-focused windows' titlebar labels. The
label is the container for the window title. When it is parentrelative,
then it uses the
[window.inactive.title.bg](#window.inactive.title.bg) which
is underneath it.

See also: [titlebar colors](#Titlebar_colors),
[window.active.label.bg](#window.active.label.bg),
[window.inactive.title.bg](#window.inactive.title.bg)

### window.inactive.handle.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | no                              |

Specifies the background for non-focused windows' handles. The handle is
the window decorations placed on the bottom of windows.

See also: [window.handle.width](#window.handle.width),
[window.active.handle.bg](#window.active.handle.bg)

### window.inactive.grip.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

Specifies the background for non-focused windows' grips. The grips are
located at the left and right sides of the window's handle. When it is
parentrelative, then it uses the
[window.inactive.handle.bg](#window.inactive.handle.bg) which
is underneath it.

See also: [window.handle.width](#window.handle.width),
[window.active.grip.bg](#window.active.grip.bg),
[window.inactive.handle.bg](#window.inactive.handle.bg)

## Active window button textures

### window.active.button.unpressed.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

Specifies the background for titlebar buttons in their default,
unpressed, state. This element is for the focused window. When it is
parentrelative, then it uses the
[window.active.title.bg](#window.active.title.bg) which is
underneath it.

See also: [titlebar colors](#Titlebar_colors),
[window.active.title.bg](#window.active.title.bg),
[window.inactive.button.unpressed.bg](#window.inactive.button.unpressed.bg)

### window.active.button.pressed.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

Specifies the background for titlebar buttons when they are being
pressed by the user. This element is for the focused window. When it is
parentrelative, then it uses the
[window.active.title.bg](#window.active.title.bg) which is
underneath it.

See also: [titlebar colors](#Titlebar_colors),
[window.active.title.bg](#window.active.title.bg),
[window.inactive.button.pressed.bg](#window.inactive.button.pressed.bg)

### window.active.button.hover.bg

| Type:           | [texture](#Textures)                                                    |
|-----------------|------------------------------------------------------------------------------------|
| Default:        | [window.active.button.unpressed.bg](#window.active.button.unpressed.bg) |
| Parentrelative: | yes                                                                                |

Specifies the background for titlebar buttons when the mouse is over
them. This element is for the focused window. When it is parentrelative,
then it uses the
[window.active.title.bg](#window.active.title.bg) which is
underneath it.

See also: [titlebar colors](#Titlebar_colors),
[window.active.title.bg](#window.active.title.bg),
[window.inactive.button.hover.bg](#window.inactive.button.hover.bg)

### window.active.button.disabled.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

Specifies the background for titlebar buttons when they are disabled for
the window. This element is for the focused window. When it is
parentrelative, then it uses the
[window.active.title.bg](#window.active.title.bg) which is
underneath it.

See also: [titlebar colors](#Titlebar_colors),
[window.active.title.bg](#window.active.title.bg),
[window.inactive.button.disabled.bg](#window.inactive.button.disabled.bg)

### window.active.button.toggled.unpressed.bg

| Type:           | [texture](#Textures)                                                |
|-----------------|--------------------------------------------------------------------------------|
| Default:        | [window.active.button.toggled.bg](#window.active.button.toggled.bg) |
| Parentrelative: | yes                                                                            |

Specifies the default background for titlebar buttons when they are
toggled - such as when a window is maximized. This element is for the
focused window. When it is parentrelative, then it uses the
[window.inactive.title.bg](#window.inactive.title.bg) which
is underneath it.

See also: [titlebar colors](#Titlebar_colors),
[window.active.title.bg](#window.active.title.bg),
[window.inactive.button.toggled.unpressed.bg](#window.inactive.button.toggled.unpresssed.bg)

### window.active.button.toggled.pressed.bg

| Type:           | [texture](#Textures)                                                |
|-----------------|--------------------------------------------------------------------------------|
| Default:        | [window.active.button.pressed.bg](#window.active.button.pressed.bg) |
| Parentrelative: | yes                                                                            |

Specifies the default background for titlebar buttons if the user is
pressing them with the mouse while they are toggled - such as when a
window is maximized. This element is for the focused window. When it is
parentrelative, then it uses the
[window.inactive.title.bg](#window.inactive.title.bg) which
is underneath it.

See also: [titlebar colors](#Titlebar_colors),
[window.active.title.bg](#window.active.title.bg),
[window.inactive.button.toggled.pressed.bg](#window.inactive.button.toggled.presssed.bg)

### window.active.button.toggled.hover.bg

| Type:           | [texture](#Textures)                                                                    |
|-----------------|----------------------------------------------------------------------------------------------------|
| Default:        | [window.active.button.toggled.unpressed.bg](#window.active.button.toggled.unpressed.bg) |
| Parentrelative: | yes                                                                                                |

Specifies the default background for titlebar buttons if the user is
pressing them with the mouse while they are toggled - such as when a
window is maximized. This element is for the focused window. When it is
parentrelative, then it uses the
[window.inactive.title.bg](#window.inactive.title.bg) which
is underneath it.

See also: [titlebar colors](#Titlebar_colors),
[window.active.title.bg](#window.active.title.bg),
[window.inactive.button.toggled.hover.bg](#window.inactive.button.toggled.hover.bg)

### window.active.button.toggled.bg

| Type:           | [texture](#Textures)                                                |
|-----------------|--------------------------------------------------------------------------------|
| Default:        | [window.active.button.pressed.bg](#window.active.button.pressed.bg) |
| Parentrelative: | yes                                                                            |

<span style="color:red">***This property is obsolete and only present
for backwards compatibility.***</span>

## Inactive window button textures

### window.inactive.button.unpressed.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

Specifies the background for titlebar buttons in their default,
unpressed, state. This element is for non-focused windows. When it is
parentrelative, then it uses the
[window.inactive.title.bg](#window.inactive.title.bg) which
is underneath it.

See also: [titlebar colors](#Titlebar_colors),
[window.inactive.title.bg](#window.inactive.title.bg),
[window.active.button.unpressed.bg](#window.active.button.unpressed.bg)

### window.inactive.button.pressed.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

Specifies the background for titlebar buttons when they are being
pressed by the user. This element is for non-focused windows. When it is
parentrelative, then it uses the
[window.inactive.title.bg](#window.inactive.title.bg) which
is underneath it.

See also: [titlebar colors](#Titlebar_colors),
[window.inactive.title.bg](#window.inactive.title.bg),
[window.active.button.pressed.bg](#window.active.button.pressed.bg)

### window.inactive.button.hover.bg

| Type:           | [texture](#Textures)                                                        |
|-----------------|----------------------------------------------------------------------------------------|
| Default:        | [window.inactive.button.unpressed.bg](#window.inactive.button.unpressed.bg) |
| Parentrelative: | yes                                                                                    |

Specifies the background for titlebar buttons when the mouse is over
them. This element is for non-focused windows. When it is
parentrelative, then it uses the
[window.inactive.title.bg](#window.inactive.title.bg) which
is underneath it.

See also: [titlebar colors](#Titlebar_colors),
[window.inactive.title.bg](#window.inactive.title.bg),
[window.active.button.hover.bg](#window.active.button.hover.bg)

### window.inactive.button.disabled.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

Specifies the background for titlebar buttons when they are disabled for
the window. This element is for non-focused windows. When it is
parentrelative, then it uses the
[window.inactive.title.bg](#window.inactive.title.bg) which
is underneath it.

See also: [titlebar colors](#Titlebar_colors),
[window.inactive.title.bg](#window.inactive.title.bg),
[window.active.button.disabled.bg](#window.active.button.disabled.bg)

### window.inactive.button.toggled.unpressed.bg

| Type:           | [texture](#Textures)                                                    |
|-----------------|------------------------------------------------------------------------------------|
| Default:        | [window.inactive.button.toggled.bg](#window.inactive.button.toggled.bg) |
| Parentrelative: | yes                                                                                |

Specifies the default background for titlebar buttons when they are
toggled - such as when a window is maximized. This element is for
non-focused windows. When it is parentrelative, then it uses the
[window.inactive.title.bg](#window.inactive.title.bg) which
is underneath it.

See also: [titlebar colors](#Titlebar_colors),
[window.inactive.title.bg](#window.inactive.title.bg),
[window.active.button.toggled.unpressed.bg](#window.active.button.toggled.unpresssed.bg)

### window.inactive.button.toggled.pressed.bg

| Type:           | [texture](#Textures)                                                    |
|-----------------|------------------------------------------------------------------------------------|
| Default:        | [window.inactive.button.pressed.bg](#window.inactive.button.pressed.bg) |
| Parentrelative: | yes                                                                                |

Specifies the default background for titlebar buttons if the user is
pressing them with the mouse while they are toggled - such as when a
window is maximized. This element is for non-focused windows. When it is
parentrelative, then it uses the
[window.inactive.title.bg](#window.inactive.title.bg) which
is underneath it.

See also: [titlebar colors](#Titlebar_colors),
[window.inactive.title.bg](#window.inactive.title.bg),
[window.active.button.toggled.pressed.bg](#window.active.button.toggled.presssed.bg)

### window.inactive.button.toggled.hover.bg

| Type:           | [texture](#Textures)                                                                        |
|-----------------|--------------------------------------------------------------------------------------------------------|
| Default:        | [window.inactive.button.toggled.unpressed.bg](#window.inactive.button.toggled.unpressed.bg) |
| Parentrelative: | yes                                                                                                    |

Specifies the default background for titlebar buttons if the user is
pressing them with the mouse while they are toggled - such as when a
window is maximized. This element is for non-focused windows. When it is
parentrelative, then it uses the
[window.inactive.title.bg](#window.inactive.title.bg) which
is underneath it.

See also: [titlebar colors](#Titlebar_colors),
[window.inactive.title.bg](#window.inactive.title.bg),
[window.active.button.toggled.hover.bg](#window.active.button.toggled.hover.bg)

### window.inactive.button.toggled.bg

| Type:           | [texture](#Textures)                                                    |
|-----------------|------------------------------------------------------------------------------------|
| Default:        | [window.inactive.button.pressed.bg](#window.inactive.button.pressed.bg) |
| Parentrelative: | yes                                                                                |

<span style="color:red">***This property is obsolete and only present
for backwards compatibility.***</span>

## Menu colors

### menu.title.text.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

Specifies the text color for menu headers.

### menu.items.text.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | white                       |

Specifies the text color for normal menu entries.

### menu.items.disabled.text.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

Specifies the text color for disabled menu entries.

### menu.items.active.text.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

Specifies the text color for normal menu entries when they are selected.

### menu.items.active.disabled.text.color

| Type:    | [color](#Colors)                                                  |
|----------|------------------------------------------------------------------------------|
| Default: | [menu.items.disabled.text.color](#menu.items.disabled.text.color) |

Specifies the text color for disabled menu entries when they are
selected.

### menu.separator.color

| Type:    | [color](#Colors)                                |
|----------|------------------------------------------------------------|
| Default: | [menu.items.text.color](#menu.items.text.color) |

The color of menu line separators. <span style="color:green">***(As of
version 3.4.7)***</span>

See also: [menu.items.text.color](#menu.items.text.color)

## Menu textures

### menu.items.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | no                              |

Specifies the background for menus.

See also: [menu.items.active.bg](#menu.items.active.bg)

### menu.items.active.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

Specifies the background for the selected menu entry (whether or not it
is disabled). When it is parentrelative, then it uses the
[menu.items.bg](#menu.items.bg) which is underneath it.

See also: [menu.items.bg](#menu.items.bg)

### menu.title.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

Specifies the background for menu headers. When it is parentrelative,
then it uses the [menu.items.bg](#menu.items.bg) which is
underneath it.

See also: [menu.items.bg](#menu.items.bg)

## OSD textures

### osd.bg

| Type:           | [texture](#Textures)                              |
|-----------------|--------------------------------------------------------------|
| Default:        | [window.active.title.bg](#window.active.title.bg) |
| Parentrelative: | no                                                           |

Specifies the background for on-screen-dialogs, such as the focus
cycling (Alt-Tab) dialog.

### osd.label.bg

| Type:           | [texture](#Textures)                              |
|-----------------|--------------------------------------------------------------|
| Default:        | [window.active.label.bg](#window.active.label.bg) |
| Parentrelative: | yes                                                          |

Specifies the background for text in on-screen-dialogs, such as the
focus cycling (Alt-Tab) dialog.

### osd.hilight.bg

| Type:           | [texture](#Textures)                                                                                                                                    |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Default:        | [window.active.label.bg](#window.active.label.bg), if it is not parentrelative. Otherwise, [window.active.title.bg](#window.active.title.bg) |
| Parentrelative: | no                                                                                                                                                                 |

Specifies the texture for the selected desktop in the desktop cycling
(pager) dialog.

### osd.unhilight.bg

| Type:           | [texture](#Textures)                                                                                                                                            |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Default:        | [window.inactive.label.bg](#window.inactive.label.bg), if it is not parentrelative. Otherwise, [window.inactive.title.bg](#window.inactive.title.bg) |
| Parentrelative: | no                                                                                                                                                                         |

Specifies the texture for unselected desktops in the desktop cycling
(pager) dialog.

## OSD colors

### osd.label.text.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

Specifies the text color for on-screen-dialogs, such as the focus
cycling (Alt-Tab) dialog.

### osd.hilight.bg.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

Specifies the color for selected desktops in the desktop cycling (pager)
dialog.

### osd.unhilight.bg.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

Specifies the color for unselected desktops in the desktop cycling
(pager) dialog.

## Text justification

### window.label.text.justify

| Type:    | [justification](#Justification) |
|----------|--------------------------------------------|
| Default: | Left                                       |

Specifies how window titles are aligned in the titlebar for both the
focused and non-focused windows.

### menu.title.text.justify

| Type:    | [justification](#Justification) |
|----------|--------------------------------------------|
| Default: | Left                                       |

Specifies how text is aligned in all menu headers.

## Text shadows

### window.active.label.text.font

| Type:    | [text shadow string](#Text_shadow_strings) |
|----------|-------------------------------------------------------|
| Default: | no shadow                                             |

Specifies the shadow for the focused window's title.

See also:
[window.inactive.label.text.font](#window.inactive.label.text.font)

### window.inactive.label.text.font

| Type:    | [text shadow string](#Text_shadow_strings) |
|----------|-------------------------------------------------------|
| Default: | no shadow                                             |

Specifies the shadow for non-focused windows' titles.

See also:
[window.active.label.text.font](#window.active.label.text.font)

### menu.items.font

| Type:    | [text shadow string](#Text_shadow_strings) |
|----------|-------------------------------------------------------|
| Default: | no shadow                                             |

Specifies the shadow for all menu entries.

### menu.title.text.font

| Type:    | [text shadow string](#Text_shadow_strings) |
|----------|-------------------------------------------------------|
| Default: | no shadow                                             |

Specifies the shadow for all menu headers.

### osd.label.text.font

| Type:    | [text shadow string](#Text_shadow_strings) |
|----------|-------------------------------------------------------|
| Default: | no shadow                                             |

Specifies the text shadow for on-screen-dialogs, such as the focus
cycling (Alt-Tab) dialog.

# Dialogs

Openbox shows dialog boxes in some situations. Two examples are:

- The exit dialog window that appears when the [exit action](Actions.md#exit) is called.
- When closing a window for a program that is not responding.

These dialogs have buttons, such as **Cancel** and **Exit**. These
buttons get their background information from
[window.active.button.\*.bg](Themes.md#active-window-button-textures).
The buttons' text color comes from
[window.active.button.\*.image.color](Themes.md#window-active-button-unpressed-image-color).

# Button images

The images used for the titlebar buttons and the submenu bullet are
1-bit xbm (X Bitmaps). These are masks where 0 = clear and 1 = colored.

The xbm image files are placed in the same directory within your theme
as the `themerc` file, as shown in the [file structure
discussion](#Theme_file_structure).

The xbm's which Openbox uses as its internal defaults are distributed
with Openbox and installed to `/usr/share/doc/openbox/xbm`.

Here are all the possible xbm files which Openbox looks for.

## Maximized button

### max.xbm

| Default: | Internal default |
|----------|------------------|

Maximize button in its default, unpressed state.

### max_toggled.xbm

| Default: | If max.xbm is present, it uses that. If not, it has a separate internal default |
|----------|---------------------------------------------------------------------------------|

Maximize button when it is in toggled state.

### max_pressed.xbm

| Default: | max.xbm, or its internal default |
|----------|----------------------------------|

Maximized button when pressed.

### max_disabled.xbm

| Default: | max.xbm, or its internal default |
|----------|----------------------------------|

Maximized button when disabled.

### max_hover.xbm

| Default: | max.xbm, or its internal default |
|----------|----------------------------------|

Maximized button when mouse is over it.

### max_toggled_pressed.xbm

| Default: | max_toggled.xbm, or max.xbm, or its internal default |
|----------|------------------------------------------------------|

Maximized button when pressed, in toggled state.

### max_toggled_hover.xbm

| Default: | max_toggled.xbm, or max.xbm, or its internal default |
|----------|------------------------------------------------------|

Maximized button when mouse is over it, in toggled state.

## Iconify button

### iconify.xbm

| Default: | Internal default |
|----------|------------------|

Iconify button in its default, unpressed state.

### iconify_pressed.xbm

| Default: | iconify.xbm, or its internal default |
|----------|--------------------------------------|

Iconify button when pressed.

### iconify_disabled.xbm

| Default: | iconify.xbm, or its internal default |
|----------|--------------------------------------|

Iconify button when disabled.

### iconify_hover.xbm

| Default: | iconify.xbm, or its internal default |
|----------|--------------------------------------|

Iconify button when mouse is over it.

## Close button

### close.xbm

| Default: | Internal default |
|----------|------------------|

Close button in its default, unpressed state.

### close_pressed.xbm

| Default: | close.xbm, or its internal default |
|----------|------------------------------------|

Close button when pressed.

### close_disabled.xbm

| Default: | close.xbm, or its internal default |
|----------|------------------------------------|

Close button when disabled.

### close_hover.xbm

| Default: | close.xbm, or its internal default |
|----------|------------------------------------|

Close button when mouse is over it.

## All-desktops button

### desk.xbm

| Default: | Internal default |
|----------|------------------|

All-desktops button in its default, unpressed state.

### desk_toggled.xbm

| Default: | If desk.xbm is present, it uses that. If not, it has a separate internal default |
|----------|----------------------------------------------------------------------------------|

All-desktops button when it is in toggled state.

### desk_pressed.xbm

| Default: | desk.xbm, or its internal default |
|----------|-----------------------------------|

All-desktops button when pressed.

### desk_disabled.xbm

| Default: | desk.xbm, or its internal default |
|----------|-----------------------------------|

All-desktops button when disabled.

### desk_hover.xbm

| Default: | desk.xbm, or its internal default |
|----------|-----------------------------------|

All-desktops button when mouse is over it.

### desk_toggled_pressed.xbm

| Default: | desk_toggled.xbm, or desk.xbm, or its internal default |
|----------|--------------------------------------------------------|

All-desktops button when pressed, in toggled state.

### desk_toggled_hover.xbm

| Default: | desk_toggled.xbm, or desk.xbm, or its internal default |
|----------|--------------------------------------------------------|

All-desktops button when mouse is over it, in toggled state.

## Shade button

### shade.xbm

| Default: | Internal default |
|----------|------------------|

Shade button in its default, unpressed state.

### shade_toggled.xbm

| Default: | If shade.xbm is present, it uses that. If not, it has a separate internal default |
|----------|-----------------------------------------------------------------------------------|

Shade button when it is in toggled state.

### shade_pressed.xbm

| Default: | shade.xbm, or its internal default |
|----------|------------------------------------|

Shade button when pressed.

### shade_disabled.xbm

| Default: | shade.xbm, or its internal default |
|----------|------------------------------------|

Shade button when disabled.

### shade_hover.xbm

| Default: | shade.xbm, or its internal default |
|----------|------------------------------------|

Shade button when mouse is over it.

### shade_toggled_pressed.xbm

| Default: | shade_toggled.xbm, or shade.xbm, or its internal default |
|----------|----------------------------------------------------------|

Shade button when pressed, in toggled state.

### shade_toggled_hover.xbm

| Default: | shade_toggled.xbm, or shade.xbm, or its internal default |
|----------|----------------------------------------------------------|

Shade button when mouse is over it, in toggled state.

## Submenu bullet

### bullet.xbm

| Default: | Internal default |
|----------|------------------|

The bullet shown in a menu for submenu entries.