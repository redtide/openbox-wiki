# x-tile

From the manpage:

> X-Tile works on any X desktop (gnome, kde, xfce, lxde…).
> The main features are: many tiling geometries, undo tiling, invert tiling order,
> cycle tiling order, optional system tray docking and menu,
> filter to avoid listing some windows, filter to check some windows by default,
> *command line interface*.

Any time I install an app that has a cl interface I think,
"Score! I can turn that into an Openbox menu!" And without further ado...

```xml
<?xml version="1.0" encoding="utf-8"?>
<openbox_menu>
<menu label="Desktop menu" id="openbox-desktop">
  <menu id="xtile-menu" label="Tile windows">
    <item label="Undo last operation">
      <action name="Execute">
        <execute>x-tile z</execute>
      </action>
    </item>
    <item label="Cycle last operation ">
      <action name="Execute">
        <execute>x-tile y</execute>
      </action>
    </item>
    <item label="Invert last operation">
      <action name="Execute">
        <execute>x-tile i</execute>
      </action>
    </item>
    <separator/>
    <item label="Vertical tiling">
      <action name="Execute">
        <execute>x-tile v</execute>
      </action>
    </item>
    <item label="Horizontal tiling">
      <action name="Execute">
        <execute>x-tile h</execute>
      </action>
    </item>
    <item label="Triangle-up">
      <action name="Execute">
        <execute>x-tile u</execute>
      </action>
    </item>
    <item label="Triangle-down">
      <action name="Execute">
        <execute>x-tile d</execute>
      </action>
    </item>
    <item label="Triangle-left">
      <action name="Execute">
        <execute>x-tile l</execute>
      </action>
    </item>
    <item label="Triangle-right">
      <action name="Execute">
        <execute>x-tile r</execute>
      </action>
    </item>
    <item label="Quarter tiling">
      <action name="Execute">
        <execute>x-tile q</execute>
      </action>
    </item>
    <item label="Custom tiling 1">
      <action name="Execute">
        <execute>x-tile 1</execute>
      </action>
    </item>
    <item label="Custom tiling 2">
      <action name="Execute">
        <execute>x-tile 2</execute>
      </action>
    </item>
    <separator/>
    <item label="Close all">
      <action name="Execute">
        <execute>x-tile c</execute>
      </action>
    </item>
    <item label="Maximize all">
      <action name="Execute">
        <execute>x-tile m</execute>
      </action>
    </item>
    <item label="Un-maximize all">
      <action name="Execute">
        <execute>x-tile M</execute>
      </action>
    </item>
    <separator/>
    <item label="Open x-tile">
      <action name="Execute">
        <execute>x-tile w</execute>
      </action>
    </item>
  </menu>
</menu>
</openbox_menu>
```

Since I have a kind of "start menu" paradigm for my applications,
I use the x-tile menu above alongside the client-list-menu as my right-click
menu in the Openbox root window (and tint2 by way of the `wm_menu` config option)
