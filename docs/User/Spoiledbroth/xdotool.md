# xdotool

See ArchWiki's [Openbox page](https://wiki.archlinux.org/index.php/openbox#Desktop_menu_as_a_panel_menu)
for details.

## Notes

1. Personally I like to employ this pattern in tint2 using the
   executor- for one this allows you to spawn a different menu when the
   icon is right clicked, and two it allows some text to accompany the
   icon (which doesn't seem possible with the tint2 launcher).
2. If you opt for, say, tint2 using the launcher method as originally
   described on ArchWiki, ensure you DO NOT enable startup notifications
   by default in your launcher. With tint2,
   ```bash
   $ cat ~/.config/tint2/tint2rg | grep startup
   ```
   should return
   ```bash
   startup_notifications = 0
   ```
