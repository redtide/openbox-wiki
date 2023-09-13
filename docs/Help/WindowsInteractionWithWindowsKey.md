# Windows keys

This proposal make use of the Super modifier key (aka Windows key) to interact
with windows in common tasks like moving, expanding, focusing, minimizing...

**Window switching (Alt+Tab style)**

```text
W-Tab       Next window (like A-Tab)
W-S-Tab     Previous window (like A-S-Tab)
```

**Directional window focus:**

```text
W-Left      focus the window at the left of current window
W-Right     focus the window at the right of current window
W-Up        focus the window at the north of current window
W-Down      focus the window at the south of current window
```

**Directional window moving:**

```text
W-C-Left    Move the window to left
W-C-Right   Move the window to right
W-C-Up      Move the window to north
W-C-Down    Move the window to south
```

**Directional window expanding:**

```text
W-S-Left    expand the window to the left
W-S-Right   expand the window to the right
W-S-Up      expand the window to the north
W-S-Down    expand the window to the south
```

**Other util keys**

```text
` W-Space     maximize window
` W-Enter     toggle full screen
` W-Esc       minimize window
` W-B         toggle decorations (border of windows)
` W-d         show desktop
```

**And this is the configuration to enable the above described shortcuts:**

```xml
<keybind key="W-Tab">
  <action name="NextWindow"/>
</keybind>
<keybind key="W-S-Tab">
  <action name="PreviousWindow"/>
</keybind>
<keybind key="W-Up">
  <action name="DirectionalFocusNorth">
    <dialog>`yes`</dialog>
  </action>
</keybind>
<keybind key="W-Down">
  <action name="DirectionalFocusSouth">
    <dialog>`yes`</dialog>
  </action>
</keybind>
<keybind key="W-Left">
  <action name="DirectionalFocusWest">
    <dialog>`yes`</dialog>
  </action>
</keybind>
<keybind key="W-Right">
  <action name="DirectionalFocusEast">
    <dialog>`yes`</dialog>
  </action>
</keybind>
<keybind key="W-C-Up">
  <action name="MoveToEdgeNorth"/>
</keybind>
<keybind key="W-C-Down">
  <action name="MoveToEdgeSouth"/>
</keybind>
<keybind key="W-C-Left">
  <action name="MoveToEdgeWest"/>
</keybind>
<keybind key="W-C-Right">
  <action name="MoveToEdgeEast"/>
</keybind>
<keybind key="W-S-Up">
  <action name="UnmaximizeFull"/>
  <action name="GrowToEdgeNorth"/>
</keybind>
<keybind key="W-S-Down">
  <action name="UnmaximizeFull"/>
  <action name="GrowToEdgeSouth"/>
</keybind>
<keybind key="W-S-Left">
  <action name="UnmaximizeFull"/>
  <action name="GrowToEdgeWest"/>
</keybind>
<keybind key="W-S-Right">
  <action name="UnmaximizeFull"/>
  <action name="GrowToEdgeEast"/>
</keybind>
<keybind key="W-space">
  <action name="ToggleMaximizeFull"/>
</keybind>
<keybind key="W-Return">
  <action name="ToggleFullscreen"/>
</keybind>
<keybind key="W-Escape">
  <action name="Iconify"/>
</keybind>
<keybind key="W-B">
  <action name="ToggleDecorations"/>
</keybind>
<keybind key="W-d">
  <action name="ToggleShowDesktop"/>
</keybind>
```
