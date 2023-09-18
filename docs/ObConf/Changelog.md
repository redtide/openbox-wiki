# Changelog

## 2.0.4

- New translations: Danish, Coatian, Finnish, Latvian, Japanese,
  Estonian, Serbian, Arabic, Dutch, Greek, Hungarian, Romanian, Polish,
  Simplified Chinese, German, and Russian translations.
- Updates to other translations.
- Fix menu theme preview rendering (including crash on some themes).
- Add new `--tab` command line option.
- Allow larger margins.
- Updates to Openbox 3.5.2 libraries.

## 2.0.3

- Added Norwegian translation
- Added Turkish translation
- Updated Traditional Czech, Chinese, Italian, and Swedish translations
- Add support for the desktop warping option
- Add support for showing the popup notification when changing desktops
- Better build support for macOS platform (no `--export-dynamic`)
- Major layout changes
- Add support for putting the move/resize popup in a fixed position on screen
- Add support for the `<monitor>` window placement option
- New icon by Myles Green
- Show an error when the configuration file is not valid, so it doesn't
  get destroyed by ObConf
- Add a `--config-file` option to specify an alternate configuration file.
- Auto-load the same configuration as Openbox is using,
  if Openbox was run with `--config-file`

## 2.0.2

- Add Traditional Chinese translation
- Add Italian translation
- Add Czech translation
- Add Spanish translation
- Add French translation
- Updated Swedish translation
- Add new `Margins` option (Margins tab)
- Add new option for centering windows when placing them
- Don't include the debian/ dir in releases
- Fix the missing `TopRight` option for the dock
- Fix the dock stacking option to match changes made in Openbox
  (it's `Above`/`Below` not `Top`/`Bottom`)
- Give the theme previews white client areas to more closely resemble a real window
- Update to Openbox 3.4.3 libraries

## 2.0.1

- Make ObConf work when the `.obt` file has been renamed (e.g. by box-look.org)
- Update Swedish translation
- Update to Openbox 3.4.2 libraries

## 2.0.0

- Add the ability to install `.obt` theme archives
- Add the ability to create `.obt` theme archives
- Double clicking a `.obt` file will launch it with ObConf,
  install the theme, and select it for both KDE and GNOME desktops
- Fix for writing invalid font entries when none existed in the config file already
- Add new dock options `showDelay` and noStrut
- Add mouse option for double click time and drag threshold
- Add option for animate iconify/restore
- Make Openbox reconfigure with communication through the X server
  rather than by PID

## 1.6.3

- Add the ability to change your fonts
- Add the `<focusLast>` config option
- When changing the number of desktops, or their names, ObConf will set
  them in the current session as well as saving them to the Openbox
  config file.
- Improve how ObConf sets the desktop names. You can leave them empty
  and it will use the default translated names from Openbox.

## 1.6.1

- Update to the Openbox 3.4 series libraries.
