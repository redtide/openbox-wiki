# Autostart

![LoginOptions.png](../assets/img/LoginOptions.png) When you log in with the
"Openbox" session type, or launch Openbox with the `openbox-session`
command, the `environment` script will be executed to set up your
environment, and the `autostart` script can launch any applications you
want to run at startup.

*When you run the `openbox` command on its own, the autostart scripts
will not run. They are run by `openbox-session` or when you log in
graphically with the "Openbox" session type.*

**Note:** Some distributions ship an "openbox" session type (for display
managers) that simply calls the openbox binary. You want to select the
entry that mentions "session."

You can use the environment script to set up any custom environment
variables you would like to use in your login session.

You can use the autostart script to launch a panel, to set your desktop
wallpaper, or anything else. Once Openbox starts, the system-wide
default script, located at `/etc/xdg/openbox/autostart`, will be run.
Then the user script at `~/.config/openbox/autostart` is run afterward.

## Setting up your environment

If you would like to set environment variables that will affect
everything run in your current session (including Openbox), you can
place them in `~/.config/openbox/environment`. Here's an example
`~/.config/openbox/environment` file:

```bash
# Set up my own path
export PATH=$HOME/bin:$PATH

# Change the language used from the system's default
export LC_CTYPE=ja_JP.utf8

# SCIM for typing non-english characters
export XMODIFIERS=@im=SCIM
export GTK_IM_MODULE=scim
export QT_IM_MODULE=scim
```

## Making your own autostart

The system can provide applications that run automatically on login
(see `/usr/libexec/openbox-xdg-autostart --list`), but you may wish to run others.

To run commands for your user account only, create and edit a file called
`~/.config/openbox/autostart`. Place any commands you want to run on startup
in the file, each ending with a `&` character.

Here's an example `~/.config/openbox/autostart` file:

```bash
# Programs that will run after Openbox has started

# Set the wallpaper
hsetroot ~/wallpaper.png &

# Run a Composite manager
xcompmgr -c -t-5 -l-5 -r4.2 -o.55 &

# SCIM support (for typing non-english characters)
scim -d &

# A panel for good times
fbpanel &
```

To run commands for all users system-wide,
place them in a similar file in `/etc/xdg/openbox/autostart`.

Make sure that you end any commands with "&" so that they are run
in the background, or any programs after it will not run.

You do *not* need to run Openbox at the end of this script.
This script is run just after Openbox has finished setting up,
and is launched by `openbox-session`.
