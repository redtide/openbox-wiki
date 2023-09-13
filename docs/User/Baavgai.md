# Baavgai

Greetings from Jersey ( be afraid ). Do folks have user pages on this wiki?
I'm like the third. Seems kind of lonely.

I'm enjoying open box, though haven't taken the plunge to go stand alone;
gnome has me by a toe or two.

I love the [pipemenus](../Community/Pipemenus/index.md), brilliant idea.
I've thrown some stuff up on the page. I'm curious as to the etiquette
of the source posting. Everyone seems to host their own, but wikis seem
made of code collecting. Also, if the host should go away, it would be
nice to have a reference in the main project. With that in mind, I'm
going to put some scripts on this page and see if the powers that be are
cool with it.

If they aren't, this stuff can also be found at
[http://chaingang.org/code/linux/obscripts](# "dead link")

I can be contacted at "baavgai at chaingang.org".

## Scripts

Any script should be considered [GPLv3](https://www.gnu.org/licenses/gpl.html).
( I'm leaving the slug off here for brevity. )
Please use them and let me know if I need to fix anything.

### "BOP" Scripts

As I started playing with pipemenus, it became clear that a lot of code
could be reused. While having everything in once script is nice, having
a basic library to do the work for new scripts also has a lot going for
it. I used all manner of prefixes, ob, pm, obpm, etc. Ultimately, I
wanted something unique that wouldn't step on other scripts. I settled
on BOP, mostly because the name amused me.

BOP is short for Baavgai's Openbox Pipemenus. Yeah, using your own name
is kind of tacky; but I've become fond of BOP. :p These are just a
sample of the files, with more on the way. Go to that web share for the
complete list. Enjoy.

Here's the library:

#### boplib.py

```py
# Baavgai's Openbox Pipemenus (BOP)
# BOP Common Library: All "BOP" files need this
# current version at http://chaingang.org/code/linux/obscripts/boplib.py

import re, binascii

FileManagerMask = "nautilus %s"

class MenuWriter:
  def __init__(self, menuPrefix):
    self.idCount = 0
    self.menuPrefix = menuPrefix

  def __GetNextMenuId(self):
    self.idCount += 1
    return 'bop_%s_%s' % (self.menuPrefix, self.idCount)

  def PrintMenuBegin(self, label):
    print '<menu id="%s" label="%s">' % (self.__GetNextMenuId(), EscEntity(label))

  def PrintMenuEnd(self):
    print '</menu>'

  def PrintMenu(self, label, func):
    self.PrintMenuBegin(label)
    func()
    self.PrintMenuEnd()

  def PrintExecMenu(self, label, execute):
    print '<menu id="%s" label="%s" execute="%s" />' % (self.__GetNextMenuId(), EscEntity(label), EscEntity(execute))


def EscEntity(text):
  for (k, v) in [['&','&'],['<','<'],['>','>'],["'",'&apos;'],['"','"'] ]:
    text = text.replace(k,v)
  return text


def EscUri(text):
  def UriRep(match):
    return binascii.unhexlify(match.group(0).replace('%',''))
  text = re.sub('\%..', UriRep, text)
  text = text.replace('_','__')
  return text

def PrintEmptyItem(label):
  print '<item label="%s"></item>' % EscEntity(label)


def PrintExecItem(label, cmd):
  print '<item label="%s">' % EscEntity(label)
  print '<action name="Execute"><execute>%s</execute></action>' % EscEntity(cmd)
  print '</item>'


def PrintFileManagerItem(label, uri):
  PrintExecItem(label, FileManagerMask % uri)


def PrintFileHeadFoot(func):
  print '<?xml version="1.0" encoding="UTF-8"?>'
  print '<openbox_pipe_menu>'
  func()
  print '</openbox_pipe_menu>'


def GetLabelPath(path):
  cmdBits = path.split('/')
  label = cmdBits[len(cmdBits)-1]
  if len(cmdBits)>2:
    server = cmdBits[2].strip()
    if (server):
      label += ' on ' + server
  return (EscUri(label), path)
```

#### bop_gbook.py

Of course, a library needs some modules. Here's a sample:

```py
#!/usr/bin/env python

# Baavgai's Openbox Pipemenus (BOP)
# BOP Gnome Bookmarks
#
# current version at http://chaingang.org/code/linux/obscripts/bop_gbook.py
# requires boplib.py found at http://chaingang.org/code/linux/obscripts/boplib.py

from boplib import *
import os

def GetMenuSequence(): return 1100

def GetMenuName(): return 'Gnome Bookmarks'

def ShowMenu():
  def ProcessBookmarkLine(line):
    bookBits = line.strip().split(" ")
    if len(bookBits)==2:
      (path, label) = bookBits
      label = EscUri(label)
    else:
      (label, path) = GetLabelPath(bookBits[0])
    PrintFileManagerItem(label, path)

  fileName = os.path.expanduser('~/.gtk-bookmarks')
  if os.path.exists(fileName):
    map(ProcessBookmarkLine, open(fileName).readlines())

if __name__ == '__main__': PrintFileHeadFoot(ShowMenu)
```

#### bop_gbook.py

The Gnome Menu. This was quirky code. In some Python implementation,
if you leave out the import gtk, it will crash real hard.

```py
#!/usr/bin/env python

# Baavgai's Openbox Pipemenus (BOP)
# BOP Gnome Menu
#
# current version at http://chaingang.org/code/linux/obscripts/bop_gmenu.py
# requires boplib.py found at http://chaingang.org/code/linux/obscripts/boplib.py

from boplib import *
import gtk, gmenu

def GetMenuSequence(): return 1000

def GetMenuName(): return 'Gnome Menu'

def ShowMenu():
  mw = MenuWriter('menu')

  def WalkMenuTreeBranch(node):
    for child in node.contents:
      if isinstance (child, gmenu.Directory):
        WalkMenuTree(child)

      if not isinstance (child, gmenu.Entry):
        continue

      if child.type == gmenu.TYPE_ENTRY:
        PrintExecItem(child.name, child.get_exec())

  def WalkMenuTree(node):
    mw.PrintMenuBegin(node.name)
    WalkMenuTreeBranch(node)
    mw.PrintMenuEnd()
  WalkMenuTreeBranch(gmenu.lookup_tree("applications.menu", gmenu.FLAGS_INCLUDE_EXCLUDED).root)

if __name__ == '__main__': PrintFileHeadFoot(ShowMenu)
```

### Scripts that don't use the boplib.py

#### diskspace.sh

I think I do a "df -h" at least once a day, sometimes many if downloading ISOs.
This is a job for awk! Does anyone use awk anymore? It's actually kind of fun.

```bash
#!/bin/sh

df -kT | awk 'BEGIN { print "<openbox_pipe_menu>";
    itemFmt="<item label=\"%s: %s\"><action name=\"Execute\"><command>true</command></action></item>\n";
    itemFmt2="<item label=\"%s: %dKB\"><action name=\"Execute\"><command>true</command></action></item>\n";
    menuFmt="<menu id=\"fs_menu_%s\" label=\"%7.2fGB %s\">\n";
    menuNum=0;
  }
  $0 ~ "dev" {
    menuNum = menuNum + 1;
    printf(menuFmt, menuNum, $5 / 1048576, $7);
    printf(itemFmt, "Filesystem", $1);
    printf(itemFmt, "Type", $2);
    printf(itemFmt2, "Size", $3/1024);
    printf(itemFmt2, "Used", $4/1024);
    printf(itemFmt2, "Avail", $5/1024);
    printf(itemFmt, "Use%", $6);
    printf(itemFmt, "Mounted on", $7);
    print "</menu>";
  }
  END { print "</openbox_pipe_menu>" }
```
