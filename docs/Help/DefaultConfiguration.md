# Default configuration

The default bindings for Openbox 3.4 include the following:

| Alt-F4                 | Close the active window
| ---                    | ---
| Alt-Space              | Show the client menu for the active window
| Alt-Tab                | Cycle between windows on the desktop
| Alt-Shift-Tab          | Cycle between windows on the desktop in reverse order
| Control-Alt-Tab        | Cycle between panel and desktop windows on the desktop
| Windows-D              | Hide all windows to show the desktop
| Windows-E              | Run the Konqueror file manager (This is an example of how to run a program with a key binding)
| Alt-Escape             | Lower the active window behind other windows, and activate the last window that was in use
| Windows-F1             | Go to the first desktop instantly
| Windows-F2             | Go to the second desktop instantly
| Windows-F3             | Go to the third desktop instantly
| Windows-F4             | Go to the fourth desktop instantly
| Control-Alt-Left       | Open the desktop switching dialog, to go to the desktop to the left of the current one
| Control-Alt-Right      | Open the desktop switching dialog, to go to the desktop to the right of the current one
| Control-Alt-Up         | Open the desktop switching dialog, to go to the desktop above the current one (This will only be useful if you use a pager to set up a desktop layout with multiple rows)
| Control-Alt-Down       | Open the desktop switching dialog, to go to the desktop below the current one (This will only be useful if you use a pager to set up a desktop layout with multiple rows)
| Shift-Alt-Left         | Open the desktop switching dialog, to go to the desktop to the left of the current one, and bring the active window with you
| Shift-Alt-Right        | Open the desktop switching dialog, to go to the desktop to the right of the current one, and bring the active window with you
| Shift-Alt-Up           | Open the desktop switching dialog, to go to the desktop above the current one, and bring the active window with you (This will only be useful if you use a pager to set up a desktop layout with multiple rows)
| Shift-Alt-Down         | Open the desktop switching dialog, to go to the desktop below the current one, and bring the active window with you (This will only be useful if you use a pager to set up a desktop layout with multiple rows)
| Alt-Left mouse button  | Move a window
| Alt-Right mouse button | Resize a window. The window is resized towards the edge that the mouse is nearest to. So use Alt-Right mouse button in the top right corner of a window to resize that corner.
| Alt-Scroll wheel       | Change desktops forward and backward

## Root menus

If you are running Openbox on its own (not inside KDE or GNOME), the following
will be available by clicking on the **desktop** (a.k.a. root window):

| Middle mouse button | Open a menu listing all your windows
| ---                 | ---
| Right mouse button  | Open a menu for launching applications (You should customize this menu to your liking)

These may or may not be available if you use a program to give you icons
on your desktop, depending on how it works.

## Focus-follows-mouse

If you enable focus-follows-mouse, the default settings are to delay
focusing windows you enter with the mouse by 200ms (1/5 of a second).
This allows you to move across windows without focusing them.

## Other configurations

There are a number of [example configuration files here](Contents.md#configuration)
which demonstrate some different ways to use Openbox.
