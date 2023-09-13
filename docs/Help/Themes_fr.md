# Themes

langue: [gb](Themes.md) | fr

Les thèmes pour OpenBox 3 sont écrits au format Xresources dans un
fichier `themerc`. le format est assez simple à apprendre et vous
disposez d'un multitude d'options.

Chaque options est détaillée ici avec leurs valeurs par défaut, les
valeurs valides acceptées.

*note : les titres et données sont en anglais pour correspondre
parfaitement à votre fichier `themerc`*

# Theme installation

les thèmes openbox s'installent dans deux dossiers:

- `/usr/share/themes` : disponible pour tous les utilisateurs
- `~/.local/share/themes` ou `~/.themes` : disponible pour un utilisateur

# Theme selection

le plus simple est d'utiliser [ObConf](../ObConf/About.md). il
existe aussi des pipemenus remplissant la même fonction.

si vous désirez modifier le thème à la main, éditer le `<name>` key dans
la section `<theme>` de votre fichier `~/.config/openbox/rc.xml`. le
[guide de Configuration](Configuration.md)(gb) est un bon endroit pour commencer.

# Theme file structure

structure de base d'un thème openbox:

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
[ObConf](../ObConf/About.md) peut créer des archives de thèmes
Openbox au format `.obt` pour partager un thème, et peut installer un
fichier `.obt` aussi facilement.

# Exemple

Ce thème n'est ici que pour l'exemple, et je ne sais même pas si il est
fonctionnel. il est ici pour vous montrer toutes les options disponibles
sue Openbox. chaque section est liée au paragraphe qui la concerne.

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

Ce sont simplement des nombres comme `1` ou `42`. ils peuvent être
entiers, négatifs ou nuls.

Exemple: <code>

    window.handle.width: 3

</code>

## Justification

détermine le placement du texte. les options acceptées: `Left`, `Center`
et `Right`.

Exemple: <code>

    menu.title.text.justify: Left

</code>

## Textures

les textures déterminent l'aspect visuel d'un élément. c'est la partie
la plus compliquée d'un fichier de thème, sans l'être trop.

les textures sont spécifiées par une chaîne de texte avec un certain
nombre de domaines. Le format est le suivant (`|` signifie "ou" et `[]`
défini un champ optionnel):

    parentrelative | ((solid | gradient gradient-type) [border] [interlaced])

voyons les textures en détail.

### Parentrelative

ParentRelative signifie que l'élément hérite des couleurs des textures
sous-jacentes. Il est, par essence, complètement transparent. Certains
éléments du thème peut être ParentRelative, et certains ne peuvent pas.
La documentation de chacun vous dira si vous pouvez utiliser
ParentRelative pour elle ou pas.

Exemple: <code>

    window.active.label.bg: Parentrelative
    window.inactive.label.bg: Parentrelative Raised

</code>

### Solid

Solid signifie que la texture est compose d'une unique couleur. la
texture **doit** être suivie d'un [color field](#Colors).

Exemple: <code>

    menu.items.bg:       Solid Flat
    menu.items.bg.color: #f8f5f2

</code>

### Gradients

la texture gradient doit être suivie d'un type. elle utilise
**impérativement** deux [color fields](#Colors): `color` and
`colorTo`.

Types de Gradients acceptés:

- Diagonal - gradient depuis le coin supérieur gauche au coin inférieur
  droit
- CrossDiagonal - gradient depuis le coin supérieur droit au coin
  inférieur gauche
- Pyramid - gradient depuis les 4 coins vers le centre
- Horizontal - gradient de la gauche vers la droite
- MirrorHorizontal - gradient depuis la gauche vers le centre, puis
  gradient renversé depuis le centre vers la droite
- Vertical - gradient depuis le haut vers le bas
- SplitVertical - gradient inversé partant du centre vers le haut et le
  bas

Exemple: <code>

    menu.title.bg:         Gradient Vertical Raised
    menu.title.bg.color:   #658fb5
    menu.title.bg.colorTo: #4d6982

</code>

#### SplitVertical gradients

SplitVertical gradients accepte deux [color fields](#Color)
additionnels en option: `color.splitTo` et `colorTo.splitTo`. ces
couleurs sont utilisées pour les bords supérieurs et inférieurs de la
texture. par défaut, les valeurs sont définies par `color` \* 5/4, and
`colorTo` \* 17/16.

Exemple: <code>

    menu.title.bg:                 Gradient SplitVertical Raised
    menu.title.bg.color:           #658fb5
    menu.title.bg.color.splitTo:   #7595b9
    menu.title.bg.colorTo:         #4d6982
    menu.title.bg.colorTo.splitTo: #557485

</code>

### Border

les bordures peuvent utiliser les textures `solid` ou `gradient`. les
options de bases sont `Flat`, `Raised` (par défaut) et `Sunken`.

Flat, ne dessine pas de bordure réelle. pour ajouter une bordure , il
lui faut absolument une [border color](#Colors) et utiliser
l'option `Flat Border`.

Exemple: <code>

    window.active.button.unpressed.bg:              Gradient Vertical Flat Border
    window.active.button.unpressed.bg.border.color: #3d4c5a

</code>

Raised et Sunken ont deux options de relief en plus. par défaut, un
relief est dessiné à l'extérieur de la bordure. si `Bevel2` est
spécifié, alors le relief sera dessiné un peu plus vers l'intérieur de
la bordure. ceci peut être utilisé pour animer les états des boutons par
exemple.

l'apparence des reliefs peut aussi être déterminée dans le thème grâce
aux options `highlight` et `shadow`:

`highlight` détermine la valeur de surbrillance appliquer à l'élément.
'0' pas de surbrillance, '256'=100% de surbrillance, '512'=200% de
surbrillance etc .. par défaut:'128'=50% en plus de luminosité.

`shadow` détermine la valuer de l'ombre. compris entre 0 (pas d'ombre)
et 256 (ombre noire). par défaut: '64'=25% de réduction de la
luminosité.

Exemple: <code>

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

Interlaced textures aka rayures horizontales. à utiliser avec une
seconde [interlaced color](#Colors).

Exemple: <code>

    window.inactive.title.bg: Solid Flat Interlaced
    window.inactive.title.bg.color: #f5f5f5
    window.inactive.title.bg.interlace.color: #f6f6f6

</code>

## Colors

les couleurs peuvent être spécifiées avec leurs noms ou leur désignation
héxadécimale GRB.

### Color names

Wikipedia décrit une [list of X11 color
names](http://en.wikipedia.org/wiki/Web_colors#X11_color_names), et plus
de détails [ici](http://en.wikipedia.org/wiki/X11_color_names).

Exemple: <code>

    menu.items.active.text.color: white
    window.active.grip.bg.color: grey40

</code>

### RGB values

Les couleurs peuvent être spécifiées par les valeurs RGB hexadécimal de
deux façons. La plus connue est à travers une syntaxe similaire à HTML,
`#​​rrggbb`. Cependant, vous pouvez également utiliser le format rgb:
`rr/bb/gg`.

Exemple: <code>

    window.active.grip.bg.color: #658fb5
    window.active.label.text.color: #fff
    menu.items.active.bg.color: rgb:90/94/98
    window.active.title.bg.color: rgb:6/9/c

</code>

Notez que `#fff` est équivalent à `#f0f0f0`, *pas à* `#ffffff`.

## Text shadow strings

Les ombrages de texte sont précisées par une chaîne de texte
spécialement formaté.

Il ya trois propriétés qui peuvent être placés dans la chaîne: `shadow`,
`shadowtint` et `shadowoffset`.

Shadow est une valeur booléenne. Par défaut, 'no'. Vous pouvez activer
une ombre pour le texte à l'aide de 'shadow=y'.

Shadowtint spécifie la valeur alpha de l'ombre ainsi que sa couleur
(noir ou blanc). Par défaut, c'est noir et 50% d'opacité. Vous pouvez
spécifier le shadowtint en utilisant 'shadowtint=70'. La teinte peut
être n'importe quel nombre entier compris entre -100 et 100. 0 signifie
0% d'opacité (invisible), 100 signifie 100% d'opacité et noir, -100
signifie 100% d'opacité et blanc.

ShadowOffset indique dans quelle mesure l'ombre doit être décalé par
rapport au texte. Sa valeur par défaut '1'. Il peut être positif pour
déplacer l'ombre en bas à droite du texte, ou négative pour la déplacer
vers le haut et à gauche du texte. Vous pouvez régler la ShadowOffset en
utilisant 'ShadowOffset=2'. 'ShadowOffset=0' placera l'ombre exactement
derrière le texte et elle ne sera pas visible.

les ombres du textes peuvent être spécifiées séparément pour chasue
élément. dans ce cas, les propriétés générales sont ignorées

Exemple: <code>

    window.active.label.text.font:shadow=y:shadowtint=70:shadowoffset=1

</code>

# Theme elements

chaque élément d'un thème correspond à un élément de menu, d'une fenêtre
etc…

le détail complet de chaque élément avec leurs spécificités sera
expliqué sous cette forme:

| Type:           | [integer](#Integers) |
|-----------------|---------------------------------|
| Default:        | 1                               |
| Valid:          | 0-100                           |
| Parentrelative: | no                              |

`Type` le type d'élément.

`Default` affiche la valeur par défaut si non spécifiées dans le thème.
si le 'default' fait référence à un autre élément, c'est celui-ci qui
servira de valeur par défaut

`Valid` indique les valeurs acceptées par les éléments, comme [integer
values](#Integers).

`Parentrelative` définit si la valeur
[Parentrelative](#Parentrelative) peut être appliquée.

## Geometry

### border.width

| Type:    | [integer](#Integers) |
|----------|---------------------------------|
| Default: | 1                               |
| Valid:   | 0 - 100                         |

détermine l'épaisseur de la bordures des fenêtres en pixels.

voir aussi:
[window.active.border.color](#window.active.border.color),
[window.inactive.border.color](#window.inactive.border.color)

### menu.border.width

| Type:    | [integer](#Integers)          |
|----------|------------------------------------------|
| Default: | [border.width](#border.width) |
| Valid:   | 0 - 100                                  |

détermine l'épaisseur de la bordure autour des menus.

voir aussi: [menu.border.color](#menu.border.color)

### menu.separator.width

| Type:    | [integer](#Integers) |
|----------|---------------------------------|
| Default: | 1                               |
| Valid:   | 1 - 100                         |

détermine l'épaisseur des séparateurs de menus.
<span style="color:green">***(As of version 3.4.7)***</span>

### menu.separator.padding.width

| Type:    | [integer](#Integers) |
|----------|---------------------------------|
| Default: | 6                               |
| Valid:   | 0 - 100                         |

détermine l'espace en pixels de chaque coté des séparateurs de menu.
<span style="color:green">***(As of version 3.4.7)***</span>

voir aussi:
[menu.separator.padding.height](#menu.separator.padding.height)

### menu.separator.padding.height

| Type:    | [integer](#Integers) |
|----------|---------------------------------|
| Default: | 3                               |
| Valid:   | 0 - 100                         |

détermine la marge supérieure et inférieure des séparateurs de menu.
<span style="color:green">***(As of version 3.4.7)***</span>

Voir aussi:
[menu.separator.padding.width](#menu.separator.padding.width)

### osd.border.width

| Type:    | [integer](#Integers)          |
|----------|------------------------------------------|
| Default: | [border.width](#border.width) |
| Valid:   | 0 - 100                                  |

détermine l'épaisseur de la bordure des fenêtres de dialogue, comme le
switch du focus (Alt-Tab).

Voir aussi: [osd.border.color](#osd.border.color)

### window.client.padding.width

| Type:    | [integer](#Integers)            |
|----------|--------------------------------------------|
| Default: | [padding.width](#padding.width) |
| Valid:   | 0 - 100                                    |

détermine l'épaisseur de la bordure latérale (droite et gauche) interne
des fenêtres. elle se dessine entre la bordure externe et le corps de la
fenêtre.

Voir aussi:
[window.active.client.color](#window.active.client.color),
[window.inactive.client.color](#window.inactive.client.color)
[window.client.padding.height](#window.client.padding.height)

### window.client.padding.height

| Type:    | [integer](#Integers)                                        |
|----------|------------------------------------------------------------------------|
| Default: | [window.client.padding.width](#window.client.padding.width) |
| Valid:   | 0 - 100                                                                |

détermine l'épaisseur de la bordure interne (haute et basse) des
fenêtres. elle se dessine entre la bordure externe et le corps de la
fenêtre.

Voir aussi:
[window.active.client.color](#window.active.client.color),
[window.inactive.client.color](#window.inactive.client.color)
[window.client.padding.width](#window.client.padding.width)

### window.handle.width

| Type:    | [integer](#Integers) |
|----------|---------------------------------|
| Default: | 6                               |
| Valid:   | 0 - 100                         |

détermine l'épaisseur de la zone de préhension. cette zone se situe en
bas de la fenêtre. une valeur de '0' masque cette zone.

Voir aussi:
[window.active.handle.bg](#window.active.handle.bg),
[window.inactive.handle.bg](#window.inactive.handle.bg),
[window.active.grip.bg](#window.active.grip.bg),
[window.inactive.grip.bg](#window.inactive.grip.bg)

### padding.width

| Type:    | [integer](#Integers) |
|----------|---------------------------------|
| Default: | 3                               |
| Valid:   | 0 - 100                         |

détermine la marge interne horizontale (et verticale si non spécifiée)
utilisée pour séparer les éléments des décorations de la fenêtre.

Voir aussi: [padding.height](#padding.height)

### padding.height

| Type:    | [integer](#Integers)            |
|----------|--------------------------------------------|
| Default: | [padding.width](#padding.width) |
| Valid:   | 0 - 100                                    |

détermine la marge interne verticale utilisée pour séparer les éléments
des décorations de la fenêtre.

Voir aussi: [padding.width](#padding.width)

### menu.overlap.x

| Type:    | [integer](#Integers)          |
|----------|------------------------------------------|
| Default: | [menu.overlap](#menu.overlap) |
| Valid:   | -100 - 100                               |

détermine le décallage horizontal entre menu et sous-menu. une valeur
positive supperpose le sous-menu au menu, une valeur négative le sépare.
<span style="color:green">***(As of version 3.4.7)***</span>

Voir aussi: [menu.overlap.y](#menu.overlap.y)

### menu.overlap.y

| Type:    | [integer](#Integers)          |
|----------|------------------------------------------|
| Default: | [menu.overlap](#menu.overlap) |
| Valid:   | -100 - 100                               |

détermine le décallage vertical entre menu et sous-menu. une valeur
positive fait descendre le sous-menu, une valeur négative le fait
monter. <span style="color:green">***(As of version 3.4.7)***</span>

Voir aussi: [menu.overlap.x](#menu.overlap.x)

### menu.overlap

| Type:    | [integer](#Integers) |
|----------|---------------------------------|
| Default: | 0                               |
| Valid:   | -100 - 100                      |

<span style="color:red">***cette propriété est obsolète et n'existe que
pour raison de compatibilité.***</span>

Voir aussi: [menu.overlap.x](#menu.overlap.x),
[menu.overlap.y](#menu.overlap.y)

## Border colors

### window.active.border.color

| Type:    | [color](#Colors)              |
|----------|------------------------------------------|
| Default: | [border.color](#border.color) |

détermine la couleur de la bordure de la fenêtre active.

Voir aussi: [border.width](#border.width),
[window.inactive.border.color](#window.inactive.border.color)

### window.active.title.separator.color

| Type:    | [color](#Colors)                                          |
|----------|----------------------------------------------------------------------|
| Default: | [window.active.border.color](#window.active.border.color) |

détermine la couleur de la bordure inférieure de la barre de titre de la
fenêtre active.

Voir aussi:
[window.inactive.title.separator.color](#window.inactive.title.separator.color)

### window.inactive.border.color

| Type:    | [color](#Colors)                                          |
|----------|----------------------------------------------------------------------|
| Default: | [window.active.border.color](#window.active.border.color) |

détermine la couleur de la bordure des fenêtres inactives.

Voir aussi: [border.width](#border.width),
[window.active.border.color](#window.active.border.color)

### window.inactive.title.separator.color

| Type:    | [color](#Colors)                                              |
|----------|--------------------------------------------------------------------------|
| Default: | [window.inactive.border.color](#window.inactive.border.color) |

détermine la couleur de la bordure inférieure de la barre de titre des
fenêtres inactives.

Voir aussi:
[window.active.title.separator.color](#window.active.title.separator.color)

### border.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

<span style="color:red">***cette propriété est obsolète et n'existe que
pour raison de compatibilité.***</span>

Voir aussi:
[window.active.border.color](#window.active.border.color),
[window.inactive.border.color](#window.inactive.border.color),
[menu.border.color](#menu.border.color)

### window.active.client.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | white                       |

détermine la couleur de la bordure interne de la fenêtre active. elle se
dessine entre la bordure externe et le corps de la fenêtre.

Voir aussi:
[window.client.padding.width](#window.client.padding.width),
[window.inactive.client.color](#window.inactive.client.color)

### window.inactive.client.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | white                       |

détermine la couleur de la bordure interne des fenêtres inactives. elle
se dessine entre la bordure externe et le corps de la fenêtre.

Voir aussi:
[window.client.padding.width](#window.client.padding.width),
[window.active.client.color](#window.active.client.color)

### menu.border.color

| Type:    | [color](#Colors)                                          |
|----------|----------------------------------------------------------------------|
| Default: | [window.active.border.color](#window.active.border.color) |

détermine la couleur de la bordure du menu.

Voir aussi: [menu.border.width](#menu.border.width)

### osd.border.color

| Type:    | [color](#Colors)                                          |
|----------|----------------------------------------------------------------------|
| Default: | [window.active.border.color](#window.active.border.color) |

détermine la couleur de la bordure des fenêtres de dialogue comme le
switch de focus (Alt-Tab).

Voir aussi: [osd.border.width](#osd.border.width)

## Titlebar colors

### window.active.label.text.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

détermine la couleur du texte de la barre de titre de la fenêtre active.

Voir aussi:
[window.inactive.label.text.color](#window.inactive.label.text.color)

### window.inactive.label.text.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | white                       |

détermine la couleur du texte de la barre de titre des fenêtres
inactives.

Voir aussi:
[window.active.label.text.color](#window.active.label.text.color)

### window.active.button.unpressed.image.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

détermine la couleur des images des boutons de la barre de titre de la
fenetre active.

Voir aussi:
[window.inactive.button.unpressed.image.color](#window.inactive.button.unpressed.image.color)

### window.active.button.pressed.image.color

| Type:    | [color](#Colors)                                                                          |
|----------|------------------------------------------------------------------------------------------------------|
| Default: | [window.active.button.unpressed.image.color](#window.active.button.unpressed.image.color) |

détermine la couleur des images des boutons lors d'un clic pour la barre
de titre de la fenetre active.

Voir aussi:
[window.inactive.button.pressed.image.color](#window.inactive.button.pressed.image.color)

### window.active.button.disabled.image.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | white                       |

détermine la couleur des images des boutons désactivés de la barre de
titre de la fenetre active.

Voir aussi:
[window.inactive.button.disabled.image.color](#window.inactive.button.disabled.image.color)

### window.active.button.hover.image.color

| Type:    | [color](#Colors)                                                                          |
|----------|------------------------------------------------------------------------------------------------------|
| Default: | [window.active.button.unpressed.image.color](#window.active.button.unpressed.image.color) |

détermine la couleur des images des boutons lors d'un survol pour la
barre de titre de la fenetre active.

Voir aussi:
[window.inactive.button.hover.image.color](#window.inactive.button.hover.image.color)

### window.active.button.toggled.unpressed.image.color

| Type:    | [color](#Colors)                                                                      |
|----------|--------------------------------------------------------------------------------------------------|
| Default: | [window.active.button.toggled.image.color](#window.active.button.toggled.image.color) |

détermine la couleur des images des boutons en mode 'toggle' (ex:
fenêtre maximisée) pour la barre de titre de la fenêtre active.

Voir aussi:
[window.inactive.button.toggled.unpressed.image.color](#window.inactive.button.toggled.unpressed.image.color)

### window.active.button.toggled.pressed.image.color

| Type:    | [color](#Colors)                                                                      |
|----------|--------------------------------------------------------------------------------------------------|
| Default: | [window.active.button.pressed.image.color](#window.active.button.pressed.image.color) |

détermine la couleur des images des boutons en mode 'toggle' (ex:
fenêtre maximisée) lors d'un clic pour la barre de titre de la fenetre
active.

Voir aussi:
[window.inactive.button.toggled.pressed.image.color](#window.inactive.button.toggled.pressed.image.color)

### window.active.button.toggled.hover.image.color

| Type:    | [color](#Colors)                                                                                          |
|----------|----------------------------------------------------------------------------------------------------------------------|
| Default: | [window.active.button.toggled.unpressed.image.color](#window.active.button.toggled.unpressed.image.color) |

détermine la couleur des images des boutons en mode 'toggle' (ex:
fenêtre maximisée) lors d'un survol pour la barre de titre de la fenetre
active.

Voir aussi:
[window.inactive.button.toggled.hover.image.color](#window.inactive.button.toggled.hover.image.color)

### window.active.button.toggled.image.color

| Type:    | [color](#Colors)                                                                      |
|----------|--------------------------------------------------------------------------------------------------|
| Default: | [window.active.button.pressed.image.color](#window.active.button.pressed.image.color) |

<span style="color:red">***cette propriété est obsolète et n'existe que
pour des raisons de compatibilités.***</span>

### window.inactive.button.unpressed.image.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | white                       |

détermine la couleur des images des boutons de la barre de titre des
fenêtres inactives.

Voir aussi:
[window.active.button.unpressed.image.color](#window.active.button.unpressed.image.color)

### window.inactive.button.pressed.image.color

| Type:    | [color](#Colors)                                                                              |
|----------|----------------------------------------------------------------------------------------------------------|
| Default: | [window.inactive.button.unpressed.image.color](#window.inactive.button.unpressed.image.color) |

détermine la couleur des images des boutons de la barre de titre des
fenêtres inactives lors d'un clic.

cette option est aussi utilisé pour le mode 'toggle' lors d'un clic pour
les fenêtres inactives.

Voir aussi:
[window.active.button.pressed.image.color](#window.active.button.pressed.image.color)

### window.inactive.button.disabled.image.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

détermine la couleur des images des boutons désactivés de la barre de
titre des fenêtres inactives.

Voir aussi:
[window.active.button.disabled.image.color](#window.active.button.disabled.image.color)

### window.inactive.button.hover.image.color

| Type:    | [color](#Colors)                                                                              |
|----------|----------------------------------------------------------------------------------------------------------|
| Default: | [window.inactive.button.unpressed.image.color](#window.inactive.button.unpressed.image.color) |

détermine la couleur des images des boutons de la barre de titre des
fenêtres inactives lors d'un survol.

Voir aussi:
[window.active.button.hover.image.color](#window.active.button.hover.image.color)

### window.inactive.button.toggled.unpressed.image.color

| Type:    | [color](#Colors)                                                                          |
|----------|------------------------------------------------------------------------------------------------------|
| Default: | [window.inactive.button.toggled.image.color](#window.inactive.button.toggled.image.color) |

détermine la couleur des images des boutons en mode 'toggle' (ex:
fenêtre maximisée) pour la barre de titre des fenêtres inactives.

Voir aussi:
[window.active.button.toggled.unpressed.image.color](#window.active.button.toggled.unpressed.image.color)

### window.inactive.button.toggled.pressed.image.color

| Type:    | [color](#Colors)                                                                          |
|----------|------------------------------------------------------------------------------------------------------|
| Default: | [window.inactive.button.pressed.image.color](#window.inactive.button.pressed.image.color) |

détermine la couleur des images des boutons en mode 'toggle' (ex:
fenêtre maximisée) lors d'un clic pour la barre de titre de la fenêtre
active.

Voir aussi:
[window.active.button.toggled.pressed.image.color](#window.active.button.toggled.pressed.image.color)

### window.inactive.button.toggled.hover.image.color

| Type:    | [color](#Colors)                                                                                              |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| Default: | [window.inactive.button.toggled.unpressed.image.color](#window.inactive.button.toggled.unpressed.image.color) |

détermine la couleur des images des boutons en mode 'toggle' (ex:
fenêtre maximisée) lors d'un survol pour la barre de titre des fenêtres
inactives.

Voir aussi:
[window.active.button.toggled.hover.image.color](#window.active.button.toggled.hover.image.color)

### window.inactive.button.toggled.image.color

| Type:    | [color](#Colors)                                                                      |
|----------|--------------------------------------------------------------------------------------------------|
| Default: | [window.active.button.pressed.image.color](#window.active.button.pressed.image.color) |

<span style="color:red">***cette propriété est obsolète et n'existe que
pour des raisons de compatibilités.***</span>

## Active window textures

### window.active.title.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | no                              |

détermine la texture de la barre de titre de la fenêtre active.

Voir aussi:
[window.inactive.title.bg](#window.inactive.title.bg)

### window.active.label.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

détermine la texture du label de la fenêtre active, la label est le fond
du titre. si 'parentrelative', alors on utilise
[window.active.title.bg](#window.active.title.bg).

Voir aussi: [titlebar colors](#Titlebar_colors),
[window.inactive.label.bg](#window.inactive.label.bg),
[window.active.title.bg](#window.active.title.bg)

### window.active.handle.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | no                              |

détermine la texture de la zone de préhension située au bas de la
fenêtre active.

Voir aussi: [window.handle.width](#window.handle.width),
[window.inactive.handle.bg](#window.inactive.handle.bg)

### window.active.grip.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

détermine la texture des zones de redimensionnements de la fenêtre
active. elles sont situées de part et d'autres de la zone de préhension
au bas des fenêtres. si 'parentrelative', on utilise
[window.active.handle.bg](#window.active.handle.bg).

Voir aussi: [window.handle.width](#window.handle.width),
[window.inactive.grip.bg](#window.inactive.grip.bg),
[window.active.handle.bg](#window.active.handle.bg)

## Inactive window textures

### window.inactive.title.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | no                              |

détermine la texture de la barre de titre des fenêtres inactives.

Voir aussi: [window.active.title.bg](#window.active.title.bg)

### window.inactive.label.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

détermine la texture du label des fenêtres inactives, la label est le
fond du titre. si 'parentrelative', alors on utilise
[window.inactive.title.bg](#window.inactive.title.bg).

Voir aussi: [titlebar colors](#Titlebar_colors),
[window.active.label.bg](#window.active.label.bg),
[window.inactive.title.bg](#window.inactive.title.bg)

### window.inactive.handle.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | no                              |

détermine la texture de la zone de préhension située au bas des fenêtres
inactives.

Voir aussi: [window.handle.width](#window.handle.width),
[window.active.handle.bg](#window.active.handle.bg)

### window.inactive.grip.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

détermine la texture des zones de redimensionnements des fenêtres
inactives. elles sont situées de part et d'autres de la zone de
préhension au bas des fenêtres. si 'parentrelative', on utilise
[window.inactive.handle.bg](#window.inactive.handle.bg).

Voir aussi: [window.handle.width](#window.handle.width),
[window.active.grip.bg](#window.active.grip.bg),
[window.inactive.handle.bg](#window.inactive.handle.bg)

## Active window button textures

### window.active.button.unpressed.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

détermine la texture des boutons de la barre de titre de la fenetre
active. si 'parentrelative', on utilise
[window.active.title.bg](#window.active.title.bg).

Voir aussi: [titlebar colors](#Titlebar_colors),
[window.active.title.bg](#window.active.title.bg),
[window.inactive.button.unpressed.bg](#window.inactive.button.unpressed.bg)

### window.active.button.pressed.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

détermine la texture des boutons de la barre de titre de la fenetre
active lors d'un clic. si 'parentrelative', on utilise
[window.active.title.bg](#window.active.title.bg).

Voir aussi: [titlebar colors](#Titlebar_colors),
[window.active.title.bg](#window.active.title.bg),
[window.inactive.button.pressed.bg](#window.inactive.button.pressed.bg)

### window.active.button.hover.bg

| Type:           | [texture](#Textures)                                                    |
|-----------------|------------------------------------------------------------------------------------|
| Default:        | [window.active.button.unpressed.bg](#window.active.button.unpressed.bg) |
| Parentrelative: | yes                                                                                |

détermine la texture des boutons de la barre de titre de la fenetre
active lors d'un survol. si 'parentrelative', on utilise
[window.active.title.bg](#window.active.title.bg).

Voir aussi: [titlebar colors](#Titlebar_colors),
[window.active.title.bg](#window.active.title.bg),
[window.inactive.button.hover.bg](#window.inactive.button.hover.bg)

### window.active.button.disabled.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

détermine la texture des boutons désactivés de la barre de titre de la
fenetre active. si 'parentrelative', on utilise
[window.active.title.bg](#window.active.title.bg).

Voir aussi: [titlebar colors](#Titlebar_colors),
[window.active.title.bg](#window.active.title.bg),
[window.inactive.button.disabled.bg](#window.inactive.button.disabled.bg)

### window.active.button.toggled.unpressed.bg

| Type:           | [texture](#Textures)                                                |
|-----------------|--------------------------------------------------------------------------------|
| Default:        | [window.active.button.toggled.bg](#window.active.button.toggled.bg) |
| Parentrelative: | yes                                                                            |

détermine la texture des boutons en mode 'toggle' (ex: fenêtre
maximisée) pour la barre de titre de la fenetre active. si
'parentrelative', on utilise
[window.inactive.title.bg](#window.inactive.title.bg).

Voir aussi: [titlebar colors](#Titlebar_colors),
[window.active.title.bg](#window.active.title.bg),
[window.inactive.button.toggled.unpressed.bg](#window.inactive.button.toggled.unpresssed.bg)

### window.active.button.toggled.pressed.bg

| Type:           | [texture](#Textures)                                                |
|-----------------|--------------------------------------------------------------------------------|
| Default:        | [window.active.button.pressed.bg](#window.active.button.pressed.bg) |
| Parentrelative: | yes                                                                            |

détermine la texture des boutons en mode 'toggle' (ex: fenêtre
maximisée) pour la barre de titre de la fenetre active lors d'un clic.
si 'parentrelative', on utilise
[window.inactive.title.bg](#window.inactive.title.bg).

Voir aussi: [titlebar colors](#Titlebar_colors),
[window.active.title.bg](#window.active.title.bg),
[window.inactive.button.toggled.pressed.bg](#window.inactive.button.toggled.presssed.bg)

### window.active.button.toggled.hover.bg

| Type:           | [texture](#Textures)                                                                    |
|-----------------|----------------------------------------------------------------------------------------------------|
| Default:        | [window.active.button.toggled.unpressed.bg](#window.active.button.toggled.unpressed.bg) |
| Parentrelative: | yes                                                                                                |

détermine la texture des boutons en mode 'toggle' (ex: fenêtre
maximisée) pour la barre de titre de la fenetre active lors d'un survol.
si 'parentrelative', on utilise
[window.inactive.title.bg](#window.inactive.title.bg).

Voir aussi: [titlebar colors](#Titlebar_colors),
[window.active.title.bg](#window.active.title.bg),
[window.inactive.button.toggled.hover.bg](#window.inactive.button.toggled.hover.bg)

### window.active.button.toggled.bg

| Type:           | [texture](#Textures)                                                |
|-----------------|--------------------------------------------------------------------------------|
| Default:        | [window.active.button.pressed.bg](#window.active.button.pressed.bg) |
| Parentrelative: | yes                                                                            |

<span style="color:red">***cette propriété est obsolète et n'existe que
pour des raisons de compatibilité.***</span>

## Inactive window button textures

### window.inactive.button.unpressed.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

détermine la texture des boutons de la barre de titre des fenêtres
inactives. si 'parentrelative', on utilise
[window.inactive.title.bg](#window.inactive.title.bg).

Voir aussi: [titlebar colors](#Titlebar_colors),
[window.inactive.title.bg](#window.inactive.title.bg),
[window.active.button.unpressed.bg](#window.active.button.unpressed.bg)

### window.inactive.button.pressed.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

détermine la texture des boutons de la barre de titre des fenêtres
inactives lors d'un clic. si 'parentrelative', on utilise
[window.inactive.title.bg](#window.inactive.title.bg).

Voir aussi: [titlebar colors](#Titlebar_colors),
[window.inactive.title.bg](#window.inactive.title.bg),
[window.active.button.pressed.bg](#window.active.button.pressed.bg)

### window.inactive.button.hover.bg

| Type:           | [texture](#Textures)                                                        |
|-----------------|----------------------------------------------------------------------------------------|
| Default:        | [window.inactive.button.unpressed.bg](#window.inactive.button.unpressed.bg) |
| Parentrelative: | yes                                                                                    |

détermine la texture des boutons de la barre de titre des fenêtres
inactives lors d'un survol. si 'parentrelative', on utilise
[window.inactive.title.bg](#window.inactive.title.bg).

Voir aussi: [titlebar colors](#Titlebar_colors),
[window.inactive.title.bg](#window.inactive.title.bg),
[window.active.button.hover.bg](#window.active.button.hover.bg)

### window.inactive.button.disabled.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

détermine la texture des boutons désactivés de la barre de titre des
fenêtres inactives. si 'parentrelative', on utilise
[window.inactive.title.bg](#window.inactive.title.bg).

Voir aussi: [titlebar colors](#Titlebar_colors),
[window.inactive.title.bg](#window.inactive.title.bg),
[window.active.button.disabled.bg](#window.active.button.disabled.bg)

### window.inactive.button.toggled.unpressed.bg

| Type:           | [texture](#Textures)                                                    |
|-----------------|------------------------------------------------------------------------------------|
| Default:        | [window.inactive.button.toggled.bg](#window.inactive.button.toggled.bg) |
| Parentrelative: | yes                                                                                |

détermine la texture des boutons en mode 'toggle' (ex: fenêtre
maximisée) pour la barre de titre des fenêtres inactives. si
'parentrelative', on utilise
[window.inactive.title.bg](#window.inactive.title.bg).

Voir aussi: [titlebar colors](#Titlebar_colors),
[window.inactive.title.bg](#window.inactive.title.bg),
[window.active.button.toggled.unpressed.bg](#window.active.button.toggled.unpresssed.bg)

### window.inactive.button.toggled.pressed.bg

| Type:           | [texture](#Textures)                                                    |
|-----------------|------------------------------------------------------------------------------------|
| Default:        | [window.inactive.button.pressed.bg](#window.inactive.button.pressed.bg) |
| Parentrelative: | yes                                                                                |

détermine la texture des boutons en mode 'toggle' (ex: fenêtre
maximisée) pour la barre de titre des fenêtres inactives lors d'un clic.
si 'parentrelative', on utilise
[window.inactive.title.bg](#window.inactive.title.bg).

Voir aussi: [titlebar colors](#Titlebar_colors),
[window.inactive.title.bg](#window.inactive.title.bg),
[window.active.button.toggled.pressed.bg](#window.active.button.toggled.presssed.bg)

### window.inactive.button.toggled.hover.bg

| Type:           | [texture](#Textures)                                                                        |
|-----------------|--------------------------------------------------------------------------------------------------------|
| Default:        | [window.inactive.button.toggled.unpressed.bg](#window.inactive.button.toggled.unpressed.bg) |
| Parentrelative: | yes                                                                                                    |

détermine la texture des boutons en mode 'toggle' (ex: fenêtre
maximisée) pour la barre de titre des fenêtres inactives lors d'un
survol. si 'parentrelative', on utilise
[window.inactive.title.bg](#window.inactive.title.bg).

Voir aussi: [titlebar colors](#Titlebar_colors),
[window.inactive.title.bg](#window.inactive.title.bg),
[window.active.button.toggled.hover.bg](#window.active.button.toggled.hover.bg)

### window.inactive.button.toggled.bg

| Type:           | [texture](#Textures)                                                    |
|-----------------|------------------------------------------------------------------------------------|
| Default:        | [window.inactive.button.pressed.bg](#window.inactive.button.pressed.bg) |
| Parentrelative: | yes                                                                                |

<span style="color:red">***cette propriété est obsolète et n'existe que
pour des raisons de compatibilités.***</span>

## Menu colors

### menu.title.text.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

détermine la couleur du texte des titres des menus et sous-menus.

### menu.items.text.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | white                       |

détermine la couleur du texte des entrées de menu.

### menu.items.disabled.text.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

détermine la couleur du texte des entrées de menu désactivées.

### menu.items.active.text.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

détermine la couleur du texte des entrées de menu lors d'un survol.

### menu.items.active.disabled.text.color

| Type:    | [color](#Colors)                                                  |
|----------|------------------------------------------------------------------------------|
| Default: | [menu.items.disabled.text.color](#menu.items.disabled.text.color) |

détermine la couleur du texte des entrées de menu désactivées lors d'un
survol.

### menu.separator.color

| Type:    | [color](#Colors)                                |
|----------|------------------------------------------------------------|
| Default: | [menu.items.text.color](#menu.items.text.color) |

détermine la couleur des séparateurs de menu.
<span style="color:green">***(As of version 3.4.7)***</span>

Voir aussi: [menu.items.text.color](#menu.items.text.color)

## Menu textures

### menu.items.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | no                              |

détermine la texture du menu.

Voir aussi: [menu.items.active.bg](#menu.items.active.bg)

### menu.items.active.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

détermine la texture de l'entrée de menu sélectionnée (qu'elle soit
activée ou non). si 'parentrelative', on utilise
[menu.items.bg](#menu.items.bg).

Voir aussi: [menu.items.bg](#menu.items.bg)

### menu.title.bg

| Type:           | [texture](#Textures) |
|-----------------|---------------------------------|
| Default:        | none                            |
| Parentrelative: | yes                             |

détermine la texture des titres des menus et sous-menus. si
'parentrelative', on utilise [menu.items.bg](#menu.items.bg).

Voir aussi: [menu.items.bg](#menu.items.bg)

## OSD textures

### osd.bg

| Type:           | [texture](#Textures)                              |
|-----------------|--------------------------------------------------------------|
| Default:        | [window.active.title.bg](#window.active.title.bg) |
| Parentrelative: | no                                                           |

détermine la texture des fenêtres de dialogue, comme le swith du focus
(Alt-Tab).

### osd.label.bg

| Type:           | [texture](#Textures)                              |
|-----------------|--------------------------------------------------------------|
| Default:        | [window.active.label.bg](#window.active.label.bg) |
| Parentrelative: | yes                                                          |

détermine la texture des labels des fenêtres de dialogue, comme le swith
du focus (Alt-Tab). le label est le fond du texte.

### osd.hilight.bg

| Type:           | [texture](#Textures)                                                                                                                                    |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Default:        | [window.active.label.bg](#window.active.label.bg), if it is not parentrelative. Otherwise, [window.active.title.bg](#window.active.title.bg) |
| Parentrelative: | no                                                                                                                                                                 |

détermine la texture du bureau actif dans le selecteur de bureaux
(pager).

### osd.unhilight.bg

| Type:           | [texture](#Textures)                                                                                                                                            |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Default:        | [window.inactive.label.bg](#window.inactive.label.bg), if it is not parentrelative. Otherwise, [window.inactive.title.bg](#window.inactive.title.bg) |
| Parentrelative: | no                                                                                                                                                                         |

détermine la texture de bureaux inactifs dans le selecteur de bureaux
(pager).

## OSD colors

### osd.label.text.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

détermine la couleur des fenêtres de dialogue, comme le swith du focus
(Alt-Tab).

### osd.hilight.bg.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

détermine la couleur du bureau actif dans le selecteur de bureaux
(pager).

### osd.unhilight.bg.color

| Type:    | [color](#Colors) |
|----------|-----------------------------|
| Default: | black                       |

détermine la couleur des bureaux inactifs dans le selecteur de bureaux
(pager).

## Text justification

### window.label.text.justify

| Type:    | [justification](#Justification) |
|----------|--------------------------------------------|
| Default: | Left                                       |

détemine le placement du texte dans la barre de titre des fenêtres
(in)actives.

### menu.title.text.justify

| Type:    | [justification](#Justification) |
|----------|--------------------------------------------|
| Default: | Left                                       |

détermine le placement du texte pour les titres de menus.

## Text shadows

### window.active.label.text.font

| Type:    | [text shadow string](#Text_shadow_strings) |
|----------|-------------------------------------------------------|
| Default: | no shadow                                             |

détermine l'ombre du titre de la fenêtre active.

Voir aussi:
[window.inactive.label.text.font](#window.inactive.label.text.font)

### window.inactive.label.text.font

| Type:    | [text shadow string](#Text_shadow_strings) |
|----------|-------------------------------------------------------|
| Default: | no shadow                                             |

détermine l'ombre du titre des fenêtres inactives.

Voir aussi:
[window.active.label.text.font](#window.active.label.text.font)

### menu.items.font

| Type:    | [text shadow string](#Text_shadow_strings) |
|----------|-------------------------------------------------------|
| Default: | no shadow                                             |

détermine l'ombre des entrées de menus.

### menu.title.text.font

| Type:    | [text shadow string](#Text_shadow_strings) |
|----------|-------------------------------------------------------|
| Default: | no shadow                                             |

détermine l'ombre des titres des menus et sous-menus.

### osd.label.text.font

| Type:    | [text shadow string](#Text_shadow_strings) |
|----------|-------------------------------------------------------|
| Default: | no shadow                                             |

détermine l'ombre du texte des fenêtres de dialogue, comme le swith du
focus (Alt-Tab).

# Dialogs

openbox affiche des fenêtres de dialogue. deux exemples:

- la fenêtre qui s'affiche quand on quitte openbox: “voulez-vous quitter
  openbox ? - annuler - quitter”.
- quand on ferme une fenêtre qui ne répond pas.

ces fenêtres ont des boutons du style *Annuler* ou *Quitter*. leur
texture est déterminée par
[window.active.button.\*.bg](Themes.md#active-window-button-textures).
la couleur du texte est déterminée par
[window.active.button.\*.image.color](Themes.md#window-active-button-unpressed-image-color).

# Button images

les images utilisées pour les boutons de la barre de titre et
l'indicateur de sous-menus (bullet) sont au format '1-bit xbm' (X
Bitmaps).

les images xbm doivent être placées dans le même dossier que le themerc
comme indiqué dans la section [Theme file
structure](#Theme_file_structure).

les images par défaut (utilisées par openbox si absentes du dossier de
thème) sont situés dans `/usr/share/doc/openbox/xbm`. chaque image doit
avoir un dénommination spécifique. voici les 'noms' d'images acceptés
par openbox:

## Maximized button

le bouton de maximisaion des fenêtres

### max.xbm

| Default: | Interne |
|----------|---------|

image du bouton de maximisation.

### max_toggled.xbm

| Default: | max.xbm ou interne |
|----------|--------------------|

image du bouton de maximisation en mode 'toggle'.

### max_pressed.xbm

| Default: | max.xbm ou interne |
|----------|--------------------|

image du bouton de maximisation lors d'un clic.

### max_disabled.xbm

| Default: | max.xbm ou interne |
|----------|--------------------|

image du bouton de maximisation désactivé (les fenêtres n'acceptant pas
la maximisation).

### max_hover.xbm

| Default: | max.xbm ou interne |
|----------|--------------------|

image du bouton de maximisation lors d'un survol.

### max_toggled_pressed.xbm

| Default: | max_toggled.xbm, max.xbm ou interne |
|----------|-------------------------------------|

image du bouton de maximisation en mode 'toggle' lors d'un clic.

### max_toggled_hover.xbm

| Default: | max_toggled.xbm, max.xbm ou interne |
|----------|-------------------------------------|

image du bouton de maximisation en mode 'toggle' lors d'un survol.

## Iconify button

le bouton d'iconification (minimisation) des fenêtres.

### iconify.xbm

| Default: | Interne |
|----------|---------|

image du bouton d'iconification.

### iconify_pressed.xbm

| Default: | iconify.xbm, ou interne |
|----------|-------------------------|

image du bouton d'iconification lors d'un clic.

### iconify_disabled.xbm

| Default: | iconify.xbm, ou interne |
|----------|-------------------------|

image du bouton d'iconification désactivé.

### iconify_hover.xbm

| Default: | iconify.xbm, ou interne |
|----------|-------------------------|

image du bouton d'iconification lors d'un survol.

## Close button

le bouton de fermeture des fenêtres.

### close.xbm

| Default: | Interne |
|----------|---------|

image du bouton de fermeture.

### close_pressed.xbm

| Default: | close.xbm, ou interne |
|----------|-----------------------|

image du bouton de fermeture lors d'un clic.

### close_disabled.xbm

| Default: | close.xbm, ou interne |
|----------|-----------------------|

image du bouton de fermeture désactivé.

### close_hover.xbm

| Default: | close.xbm, ou interne |
|----------|-----------------------|

image du bouton de fermeture lors d'un survol.

## All-desktops button

le bouton de fixation de la fenêtre (aka “sticky”) pour rendre la
fenêtre visible sur tous les bureaux.

### desk.xbm

| Default: | Interne |
|----------|---------|

image du bouton sticky.

### desk_toggled.xbm

| Default: | desk.xbm ou interne |
|----------|---------------------|

image du bouton sticky en mode 'toggle'.

### desk_pressed.xbm

| Default: | desk.xbm ou interne |
|----------|---------------------|

image du bouton sticky lors d'un clic.

### desk_disabled.xbm

| Default: | desk.xbm ou interne |
|----------|---------------------|

image du bouton sticky désactivé.

### desk_hover.xbm

| Default: | desk.xbm ou interne |
|----------|---------------------|

image du bouton sticky lors d'un survol.

### desk_toggled_pressed.xbm

| Default: | desk_toggled.xbm, desk.xbm ou interne |
|----------|---------------------------------------|

image du bouton sticky en mode 'toggle' lors d'un clic.

### desk_toggled_hover.xbm

| Default: | desk_toggled.xbm, desk.xbm ou interne |
|----------|---------------------------------------|

image du bouton sticky en mode 'toggle' lors d'un survol.

## Shade button

le bouton d'enroulement des fenêtres, afin de n'afficher que la barre de
titre

### shade.xbm

| Default: | Interne |
|----------|---------|

image du bouton d'enroulement des fenêtres.

### shade_toggled.xbm

| Default: | shade.xbm ou interne |
|----------|----------------------|

image du bouton d'enroulement en mode 'toggle'.

### shade_pressed.xbm

| Default: | shade.xbm ou interne |
|----------|----------------------|

image du bouton d'enroulement lors d'un clic.

### shade_disabled.xbm

| Default: | shade.xbm ou interne |
|----------|----------------------|

image du bouton d'enroulement lors d'un clic.

### shade_hover.xbm

| Default: | shade.xbm ou interne |
|----------|----------------------|

image du bouton d'enroulement lors d'un survol.

### shade_toggled_pressed.xbm

| Default: | shade_toggled.xbm, shade.xbm ou interne |
|----------|-----------------------------------------|

image du bouton d'enroulement en mode 'toggle' lors d'un clic.

### shade_toggled_hover.xbm

| Default: | shade_toggled.xbm, shade.xbm ou interne |
|----------|-----------------------------------------|

image du bouton d'enroulement en mode 'toggle' lors d'un survol.

## Submenu bullet

### bullet.xbm

| Default: | Interne |
|----------|---------|

image du bouton d'indication de sous-menus.

------------------------------------------------------------------------

traduction: [arpinux](User:Arpinux) 14:39, 24 April 2013
(EDT)