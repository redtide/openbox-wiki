# Wallpaper

Openbox does not natively support wallpapers,
but wallpapers can be displayed with [Nitrogen][2].

## Different wallpaper on every workspace

A different background for each workspace might be desired to provide
orientation, to easily know which [desktop][1]
you are on.
A script is given here: [A way to have per desktop or random wallpapers in Openbox][3].
Add to `autostart.sh`. There may be an issue with resource usage,
depending how often you switch desktops.

Some older, sometimes incomplete solutions, in case the above isn't what is needed:

- [Set different background images per virtual desktop][4].
  "have a desktop type window on each desktop that simply displayed
  whatever you wanted, and it would have that effect"
- [Using feh][5].
- [Using conky][6] (same thread as the feh idea).
  This will only change the wallpaper when conky updates,
  and it will update every time conky updates, adding to CPU usage.
  There is a \[suggestion\] to use the $execi or
  $texeci command to check whether the desktop is the same as when
  last checked, hopefully using less resources, but no code is given.

- [Different wallpaper on every workspace - solved][7] -
  works for keyboard combinations, not for changing desktop by mouse.

## Rotating desktop wallpapers

See: [Rotating desktop wallpapers][8]


[1]: Configuration.md#desktops
[2]: https://github.com/l3ib/nitrogen/
[3]: https://crunchbang.org/forums/topic/18034/a-way-to-have-per-desktop-or-random-wallpapers-in-openbox/
[4]: https://icculus.org/pipermail/openbox/2009-April/006160.html
[5]: https://crunchbang.org/forums/post/146107/#p146107
[6]: https://crunchbang.org/forums/post/147331/#p147331
[7]: https://crunchbang.org/forums/topic/4538/different-wallpaper-on-every-workspace-solved/
[8]: https://crunchbang.org/forums/post/2237/
