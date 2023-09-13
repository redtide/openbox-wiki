# Actions

This is a chronological brain dump from top to bottom, so should really
be read from bottom up maybe.

- singleword = action
- key:value = set option for last seen action
- { } = for placing an action (or list of) in an action
- " " = is a string, not an action
- can use \\ \\ *a**n**d* inside any string

## Filters

- \[ \] = setting target(s) for an action, tries them left to right
  until it finds one that matches at least 1 window. separate target
  options by ",". all options inside one set of \[\] must apply to
  choose a window.
  - some targets are:
    - target - is the focused window, or the window targetted by
      an interractive action
    - focus - is the focused window (ignores the fact you're
      targetting something else in alt-tab for instance
    - title="foo" - pattern match foo against all titles
    - type="foo" - pattern match foo against all types
    - (basically anything we test in the app-specific rules..)
    - desktop=1 - match against the window's current desktop (a
      number or "all")
    - ifviewing=3 - match against current desktop (filters all or
      none)
    - visible - a flag that the window is on the currently visible
      desktop
    - not<test> - inverts the other test (maybe not <test>)

for bind action, chroot means when a breakchroot is hit, any bindings
inside are removed

`bind key:C-A-a chroot:yes actions:{ bind key:Escape actions:breakchroot`
`                                    bind key:Left actions:{moverelative x:-5}`
`                                    bind key:Right actions:{moverelative x:5}`
`                                    bind key:Up actions:{moverelative y:-5}`
`                                    bind key:Down actions:{moverelative y:5}`
`                                  }`

we decided not to do chroots this way. **WE DIDN'T DECIDE HOW TO
REPRESENT THEM YET.** or how to do keybindings in general. the action
approach seems decent though.

Possible -unixcommand syntax

`bind -key=A-Tab -actions={nextwindow -finalactions={focus unshade raise -app=yes}}`

Examples..

`bind key:W-a actions:togglemaximizefull`
`bind key:A-Escape actions:{lower app:yes focustobottom unfocus}`
`bind key:A-Tab actions:{nextwindow finalactions:{focus unshade raise app:yes}}`
`bind key:A-S-Tab actions:{previouswindow finalactions:{focus unshade raise app:yes}}`
`bind key:W-Tab actions:{showmenu menu:client-list-combined-menu}`
`bind key:W-F10 actions:{execute command:"gnome-screensaver-command -l"}`
`bind key:W-F11 actions:reconfigure`
`bind key:W-F12 actions:restart`
`bind key:C-A-Left actions:{desktopleft dialog:no wrap:no}`
`bind key:C-A-Up actions:{desktopup dialog:no wrap:no}`
`bind key:S-A-Up actions:{sendtodesktopup dialog:no wrap:no follow:yes}`
`bind key:A-F4 actions:{close}`
`bind key:A-F4 actions:{close [target]}   # target = default`
`bind key:A-S-F4 actions:{close [title="*Google Chrome", desktop=2]}  # chrome windows on desktop 2`
`bind key:A-S-F4 actions:{close [desktop=1] [desktop=2]}  # all windows on desktop 1. if none match, then all windows on desktop 2`
`bind key:Print actions:{execute command:"gnome-screenshot"}`
`bind key:W-d actions:{toggleshowdesktop}`
`bind key:W-S-Right actions:{directionalcyclewindows direction:right}`
`bind key:W-S-Left  actions:{directionalcyclewindows direction:left}`
`bind key:W-S-Up    actions:{directionalcyclewindows direction:up}`
`bind key:W-S-Down  actions:{directionalcyclewindows direction:down}`

`reconfigure  # an action with no options`
`restart command:"metacitylol"  # an action with one option`
`nextwindow finalactions:{focus unshade raise app:yes}  # nested actions`
`# execute action outside of a bind action`
`execute startupnotify:true startupname:Konqueror command:"kfmclient openProfile filemanagement"  # multiple options`

`close [target]   # target = default`
`close [title="*Google Chrome", desktop=2]  # chrome windows on desktop 2`
`close [desktop=1] [desktop=2]  # all windows on desktop 1. if none match, then all windows on desktop 2`

`togglemaximizefull`
`moverelative x:-5`
`moverelative y:-5`
`moverelative y:-5`
`moverelative y:-5`

Have alias action to build composite actions (macros)

`alias name:_foo actions:{foo bar baz}`

`if [title="* GIMP", desktop=8, viewing=8] actions:{foo bar}`

`alias name:_myif actions:`
`  [viewing=8, desktop=8] {`
`    [title="* GIMP"] {`
`      moveresizeto x:69 y:0 width:1373 height:1005`
`      sendkeyevent usetarget:no key:C-j`
`    }`
`    [locked=no, notitle="* GIMP" title="Toolbox - *"]`
`      lock`
`  }`

Attempt at an Else:

`[viewing=8, desktop=8] {`
`  [title="* GIMP"] nextwindow`
`}`
`| [visible] nextwindow`

`alias name:_myif actions:{`
`  moveresizeto [viewing=8, desktop=8, title="* GIMP"] x:69 y:0 width:1373 height:1005`
`  sendkeyevent [viewing=8, desktop=8, title="* GIMP"] usetarget:no key:C-j`
`  lock         [locked=no notitle="* GIMP" title="Toolbox - *"]}`
`}`

Attempt to group filters on actions by use of a chain action:

`chain [viewing=8,desktop=8]`
`  a:{chain [title="* GIMP"]`
`       a:{moveresizeto x:69 y:0 width:1373 height:1005`
`          sendkeyevent usetarget:no key:C-j}`
`     | lock [locked=no, title="Toolbox - *]}`

`[target] {moveresizeto a:foo} | stuff`
`[desktop=2] movetodesktop desktop:4 | [desktop=1] {stuff otherstuff}`
`[foo] bar | baz`

Do filters stack as parsing continues on a line? We decided no.

What about OR in filters?

`[foo] bar | [lal] bar | baz => [foo | lal] bar | baz`

`[a,b | c,d] foo | bar`
`[a, (b|c), d] foo | bar`

# PROPOSED ACTION LANGUAGE

In BNF like thing:

`TEST       := KEY=VALUE | KEY   # eg. locked or desktop=1. See `[`Filters`](#Filters)`.`
`ACTION     := [FILTER] ACTION ACTIONELSE | ACTIONNAME ACTIONOPTS | {ACTIONLIST}`
`ACTIONLIST := ACTION ACTIONLIST | ACTION`
`ACTIONELSE := nil | \| ACTION`
`FILTER     := FILTERORS`
`FILTERORS  := FILTERANDS \| FILTERORS | FILTERANDS`
`FILTERANDS := TEST, FILTERANDS | TEST`
`ACTIONOPTS := ACTIONOPT ACTIONOPTS | ACTIONOPT`
`ACTIONOPT  := ATTRIBUTE:WORD | ATTRIBUTE:STRING | ATTRIBUTE:{ACTIONLIST}        `
`WORD   := string of text without any spaces                                     `
`STRING := "TEXT" | (TEXT)`
` where TEXT is a string, any occurance of the closing quote character must     `
` be escaped by an backslash.                                                   `
` \\ `` and \" are all valid escaped characters.                         `

In English like thing:

`an ACTIONSPOT can hold an ACTION, an ACTIONLIST, or a FILTER followed by another ACTIONSPOT.`
`  it may be followed by a | ELSE, where ELSE is an ACTIONSPOT which is only run if the prior action spot's filter`
`  returned an empty list of windows.`
`an ACTIONLIST is a list of 1 or more space-separated ACTIONSPOTS inside {}.`
`a FILTER is a [] with tests (eg foo=bar) inside delimited by , for AND and | for OR. AND has higher`
`  precedence.`
`an ACTION is a name (no spaces) and a space-separated list of key:value pairs to assign to the ACTION.`
`  the value is a WORD, a STRING or an ACTIONLIST.`
`a WORD is a string of text with no space and does not start with a '(' '"' or '{' character.`
`a STRING is a string of text quoted with "" or ().  the ending quoting character and '\' must be escaped`
`  inside the STRING, and `` \" or \\ are all valid escaped characters.`
`  Unrecognized escape sequences are simply dropped from the string with a warning to the user.`

Example using bind to also be an action:

`bind key:M-r actions:{[la] foo | {bar etc:(yay)}`
`                      morethings`
`                     }`

Bind actions should not persist though! Need to be recreated at startup,
tho they can be injected at runtime.

note: OR precedence can be achived by splitting into nested filters:

` [a,b] [c|d] foo   => if (a&b)&(c|d) then foo`

Examples:

`execute startupnotify:true startupname:Konqueror command:(kfmclient openProfile filemanagement)`
`execute startupnotify:true startupname:Konqueror command:"kfmclient openProfile filemanagement"`

`[ifviewing=8, desktop=8] {`
`  [title="* GIMP"] {moveresize sendkey}`
`  [title="Toolbox - *", nottitle="* GIMP", locked=no] lock`
`}`

## Functionality

[Filters](#filters) are used to create a list of windows.
The default filter is *\[target\]* meaning only the targetted window is matched.
Each action is run and passed a list of windows matched by the filters applied to it.

## Keybindings, Mousebindings and Lions, Oh my.

We need to decide
1. how to do keybinds, esp chroots.
2. how to do mousebinds, esp contexts (no xml tree anymore)

## Filters as functions

- Mikachu thinks he might want filters to be able to act on other filters.
  For instance, to get all windows matching title,
  then get all windows in group with each of them.
- That doesn't work with the standard union/intersection between filters.
- We would need a filter to be able to take a set of clients as its parameter such as

`[group=[title="foo"]] dostuff`
`  OR`
`[group=[focused]] dostuff`

It is possible that some special cases for group would be enough though,
without this passing sets around, such as

`[group=focus] dostuff`
`[group=target] dostuff; [group] dostuff  # synonymous`

## Boolean filters

Some filters return a boolean value, such as "on desktop 3". These
filters return either ALL or EMPTY.

- ALL is a special client set that is considered non-empty for truth
  testing, regardless of if there are windows in it.
- EMPTY is the empty set, which would test false for truth testing.
- Anything union with ALL will give back ALL.

`[ondesktop=3|any set here] -> will give back ALL when on desktop 3.`

ALL can be implemented with a flag in the ObClientSet,
which saves copying all the ObClients also.

`[ondesktop=3,windowdesktop=2] stuff | other`

The above should always run stuff (even with an empty set if
windowdesktop=2 returns EMPTY) when on desktop 3. And always run other
when not.
