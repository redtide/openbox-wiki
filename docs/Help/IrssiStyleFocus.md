# IRSSI style focus

Irssi-style window switching is the use of a modifier key + a number key
to switch to a specific window. For example, one could set up W-3 to
switch to the third open window. This is easily accomplished in Openbox
by setting up keybindings to execute this little
[external focus-switching program](https://icculus.org/openbox/tools/irssi-focus.c)
like so:

```xml
<keybind key="W-1">
  <action name="execute">
    <execute>irssi-focus 0</execute>
  </action>
</keybind>
<keybind key="W-2">
  <action name="execute">
    <execute>irssi-focus 1</execute>
  </action>
</keybind>
```

and so on.
