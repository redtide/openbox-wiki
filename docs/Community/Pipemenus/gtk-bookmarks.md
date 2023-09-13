# gtk-bookmarks

Originally appeared on the `david.chalkskeletons.com/scripts/` repository.

Retrieved from the depths of the [Wayback Machine](https://web.archive.org/web/20150215210315/http://david.chalkskeletons.com/scripts/bookmarks.sh)

```bash
#!/bin/bash

echo '<openbox_pipe_menu>'

filemanager="nautilus"

for bookmark in `sed 's/[ ][^ ]*$//' .gtk-bookmarks
` ; do
  echo '<item label="'`basename ${bookmark}`'">'
  echo '<action name="Execute"><execute>'
  echo "$filemanager ${bookmark}"
  echo '</execute></action>'
  echo '</item>'
done

echo '</openbox_pipe_menu>'
```
