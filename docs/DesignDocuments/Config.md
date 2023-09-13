# Config

Key points:

- bindings in separate human editable file
  - `~/.config/openbox/keys` ?
  - `~/.config/openbox/mouse` ?
- menus in separate human editable file
  - `~/.config/openbox/menu` ?
- per app settings in separate human editable file
  - `~/.config/openbox/windows` ?
- these files can remain XML since we have a nice parser for that
- config options stored in machine file
  - `~/.cache/openbox/settings`
  - plaintext so mika can edit it (and for when debugging)
  - unrecognized stuff in the file is not deleted when saving
    - lets multiple versions of openbox share the same file
- `--config-file` will be weird now
  - maybe a `--config-name` instead and it uses one of
    - `~/.config/openbox-{name}/*` and `~/.cache/openbox-{name}/*`
    - `~/.config/openbox/name/*` and `~/.cache/openbox/name/*`
    - `~/.config/openbox/*-name` and `~/.cache/openbox/*-name`
- options are saved when they are changed (power failure shouldnt lose settings)
- rc script on startup is possible.. not sure it is useful
  - things like current desktop can be saved on shutdown
- easiest to use current config format for machine writable file (code exists)
  - \*could\* use it for human editable files too (even tho xml not nice..)

From August 2, 2011:

```text
04:37 (xor) menus and perapp settings probably both stay xml
04:37 (xor) i dont think ppl want to set up perapp settings with action commands
04:37 (Mikachu) what about other options?
04:37 (xor) theyll be set thru actions
04:37 (xor) so your rc will be a script
04:38 (Mikachu) i see
04:38 (xor) oh
04:38 (xor) actually i take that back
04:38 (xor) i think your rc wont exist
04:38 (xor) and you just change settings and ob saves thems
04:38 (xor) well
04:38 (xor) except bindings
04:39 (xor) bindings/perapp/menus won't be saved
04:39 (Mikachu) where would it save them?
04:39 (xor) but other options we can just cache them
04:39 (xor) in ~/.cache/openbox i figure
04:39 (Mikachu) that sounds yucky to me
04:39 (xor) whyfor
04:39 (xor) that way you change something and it just stays
04:39 (Mikachu) just does
04:39 (xor) which is my ultimate goal
04:40 (Mikachu) it feels a bit gnome-y to hide the settings in some weird dir
                making it hard to figure out what's going on
04:40 (xor) but if you expose them all thru some UI then its not really hidden
04:40 (xor) gnome hides them all and doesnt give a way to change them without
            going in the hidden shit and editing
04:41 (Mikachu) also it makes --config-file weird
04:41 (xor) yeh probably change it
04:41 (xor) config-name or something
04:42 (xor) and ~/.config/openbox-{config-name} ~/.cache/openbox-{config-name}
            get used
04:42 (xor) or something
04:42 (xor) or a subdir
04:42 (xor) i want a program like obconf to be able to change settings without
            editing files
04:43 (xor) cuz that shit is hacky
04:43 (xor) mixing human and machine generated stuff in 1 file
04:43 (Mikachu) if the rc is a bunch of actions that set options, won't that
                overwrite whatever obconf sets?
04:43 (xor) yeh it would
04:43 (Mikachu) so..
04:44 (xor) so dont set stuff like that in your rc
04:44 (xor) or
04:44 (xor) we dont make an rc at all
04:44 (xor) and make a bindings file
04:44 (xor) and an windowsettings file
04:44 (xor) and done
04:44 (xor) but i liked the idea of being able to set your current desktop to 3
            or something in your rc
04:45 (xor) then again that can get saved easily too
04:45 (xor) right now it needs a session manager to save anything
04:45 (xor) and most people dont use one and its so deprecated now anyway
04:45 (xor) id like ob to save things more intelligently on its own
04:45 (Mikachu) can we make this magic file human readable at least?
04:45 (Mikachu) so people who don't want gtk can still edit the config
04:45 (xor) and just add in what it can with a session manager
04:46 (xor) yeh it can be xml maybe :)
04:46 (xor) you can edit the config by running an action
04:46 (xor) anyway
04:46 (xor) setopt focusnew:true
04:46 (xor) done
04:46 (Mikachu) so to edit your config you have to edit your rc to set the
                config, restart openbox, then remove it again
04:46 (Mikachu) sounds convoluted
04:47 (xor) and you can do that from a shell (or from within openbox maybe)
04:47 (xor) no
04:47 (xor) you just run that and youre done
04:47 (xor) and its saved
04:47 (xor) no reconfigure no restart no anything
04:48 (xor) also could make a menu with all the options - back to blackbox
            style - probably a pipe menu..
04:48 (Mikachu) only boolean options
04:48 (xor) submenus
04:49 (xor) or make text entry menu widget :p
04:49 (Mikachu) how would you let me change the activewindow font from a menu?
04:49 (Mikachu) heh
04:49 (xor) show a menu of fonts
04:49 (Mikachu) i like being able to vcs my config
04:50 (xor) because of your bindings
04:50 (xor) which you could still
04:50 (Mikachu) and if changing an option causes a problem that makes it hard 
                to change it back via the ui, it needs to be easy to restore
                the config from outside openbox
04:50 (xor) you can
04:50 (xor) obrun setopt focusnew:false
04:50 (xor) from a shell
04:50 (xor) or whatever it would be called
04:50 (xor) you can run any action from shell scripts
04:50 (xor) (in future)
04:51 (Mikachu) without a running openbox instance?
04:51 (xor) hm
04:51 (xor) no
04:51 (xor) are you concerned about crashes ?
04:51 (Mikachu) i just really like editing text file configs i suppose
04:52 (xor) cuz i think it should save the config on log out so a crash wouldnt
            save the bad option
04:52 (Mikachu) as long as there is one of those i will survive
04:52 (xor) hehe okay
04:52 (xor) for apps that you run and close i think they can make sense
04:52 (xor) but openbox is a long-running process, it never closes unless you
            reboot basically
04:52 (Mikachu) there are probably many people who never log out, just start
                openbox after reboot due to power failure :P
04:52 (Mikachu) it would be a pain if that never saved options
04:52 (xor) i spose so
04:53 (xor) thats fine then
04:53 (xor) since we can always change them by hand when debugging
04:53 (Mikachu) it would make the most sense to keep the current format then
04:54 (xor) yeh probably so
04:54 (Mikachu) and just excise bindings to the new file
04:54 (xor) then the code is already there
04:54 (xor) good point
04:54 (Mikachu) plus i can drop my rc in the cache dir and it will work :P
04:54 (xor) :)
04:54 (xor) with some cutting
04:54 (Mikachu) yeah make sure to not drop elements you don't recognize when
                saving
04:54 (Mikachu) because then running an old version would kill any new options
04:55 (xor) hm, yeh
04:55 (xor) but then removing/renaming options would grow the file until it
            took over your harddrive
04:55 (Mikachu) haha
04:56 (Mikachu) but then old and new versions will work on the same file, and
                share the options they both know about
04:56 (Mikachu) i don't think there's ever any reason to rename an option though
04:56 (Mikachu) since it's only visible in the cache file
04:56 (xor) yeh true
04:56 (xor) should write this stuff
04:56 (Mikachu) plus it would lose the value on update then
```
