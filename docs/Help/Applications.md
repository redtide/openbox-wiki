# Settings for specific windows (Per-application settings)

Per-application settings are specified in the `<applications>` section of `rc.xml`

## Syntax

A per-app setting is specified as follows:

```xml
<applications>
  ...
  <application name="NAME" class="CLASS" role="ROLE" title="TITLE" type="TYPE">
    ...PROPERTIES...
  </application>
  ...
</applications>
```

A complete list of possible properties to set is in the
[default rc.xml file](https://git.icculus.org/?p=mikachu/openbox.git;a=blob_plain;f=data/rc.xml;hb=master),
which you can find in `/etc/xdg/openbox/rc.xml`.

## Finding the class, name, role, title and type parameters

Per-application settings let you match on what we call class, name, role, title
and type. These can all be determined with the `obxprop` utility.
Run `obxprop | grep "^_OB_APP"` to see the value of these five properties.
The output will look like

```c
_OB_APP_TYPE(UTF8_STRING) = "normal"
_OB_APP_CLASS(UTF8_STRING) = "Google-chrome"
_OB_APP_NAME(UTF8_STRING) = "google-chrome"
_OB_APP_ROLE(UTF8_STRING) =
_OB_APP_TITLE(UTF8_STRING) = "Google Chrome"
```

You have to specify at least one of class and name. Optionally, you may
specify more than one, in which case they must all match for the rule to
be applied. You may also optionally specify role and type. Note that the
title matched is the one when the window was mapped. Many programs set
the title just after mapping the window which means the value Openbox
sees as it is determining which rules to apply is sometimes empty or
something like "Untitled". The `_OB_APP_TITLE` property will show the
value that Openbox used, not the current title.

## Matching windows with wildcards

When specifying the name, class, or role for a rule, you can use simple
wildcard matching with the `*` and `?` characters. A `*` matches any
number of characters and a `?` matches any single character.

## Matching against multiple rules

As well, multiple rules can be applied to the same window. This lets you
do more with less writing. For instance you could write one rule to
match against all windows and then later rules could further change
things for more specific windows. The rules are matched in the order
they appear in your configuration file, so later rules will override
previous rules if they both specify the same setting for a window.

## Example of per-app settings

Here's an example from rc.xml that uses wildcards, and matches multiple
rules against windows:

```xml
<applications>
  <!-- match all windows, and remove their decorations -->
  <application class="*">
    <decor>no</decor>
  </application>
  <!-- orage does get decorations though.
        calender app, see http://www.xfce.org/projects/orage/ -->
  <application class="Orage">
    <decor>yes</decor>
  </application>
  <!-- my xterm with screen in it must always be on desktop 2,
        maximized and below everything else -->
  <application name="screen">
    <desktop>2</desktop>
    <maximized>yes</maximized>
    <layer>below</layer>
  </application>
  <!-- i want firefox on desktop 3 and maximized -->
  <application name="Firefox*">
    <desktop>3</desktop>
    <maximized>yes</maximized>
  </application>
  <!-- MPlayer will follow me around when i switch desktop.
        that way i can always watch my vids when coding.
        same goes for Realplayer -->
  <application class="MPlayer">
    <desktop>all</desktop>
    <layer>above</layer>
  </application>
  <application class="Realplay.bin">
    <desktop>all</desktop>
    <layer>above</layer>
  </application>
  <!-- i want nwn always maximized, same for openttd -->
  <application name="Neverwinter Nights Client">
    <maximized>yes</maximized>
  </application>
  <application class="openttd">
    <maximized>yes</maximized>
  </application>
  <!-- A is for Amarok, A is the 1st letter in the alphabet, so
        move Amarok to the first desktop -->
  <application class="Amarokapp">
    <desktop>1</desktop>
    <maximized>yes</maximized>
  </application>
  <!-- Easytag is obviously something which belongs on desktop 6, duh -->
  <application name="easytag">
    <desktop>6</desktop>
    <maximized>yes</maximized>
  </application>
</applications>
```

## Graphically managing per-application settings

[OBApps](https://sourceforge.net/projects/obapps/) is a GUI tool for
creating and editing per-application settings. It allows you to click on
a window to create a matching rule and to easily set all the properties
documented in the example configuration.
