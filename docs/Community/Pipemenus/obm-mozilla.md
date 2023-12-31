# obm-mozilla

Originally appeared on the david.chalkskeletons.com/scripts/ repository.

Retrieved from the depths of the [Wayback Machine](https://web.archive.org/web/20130914074350/http://david.chalkskeletons.com/scripts/obm-moz).

```py
#!/usr/bin/env python -O
#########################################################################
#  Copyright 2005 Manuel Colmenero
#
#    This program is free software; you can redistribute it and/or modify
#    it under the terms of the GNU General Public License as published by
#    the Free Software Foundation; either version 2 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU General Public License for more details.
#
#    You should have received a copy of the GNU General Public License
#    along with this program; if not, write to the Free Software
#    Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA
#
########################################################################
#
# a mozilla bookmarks to openbox menus translator
#

import obxml, sys, os
from HTMLParser import HTMLParser
from optparse import OptionParser

class MozParser(HTMLParser, obxml.ObMenu):

    def init(self):
        self.stack = [None]
        self.data = ""
        self.newPipe()
        self.href = ""
        self.root = ""
        self.started = False
        self.finished = False
        self.browser = "firefox"

    def openFile(self,filename):
        try:
            f = open(filename)
        except:
            mp.createItem(None, "Couldn't open file!", "Execute", "true")
            return

        mp.feed(f.read())
        f.close()

    def handle_data(self, data):
        if self.finished: return

        d = data.strip()
        if d != "":
            self.data = unicode(d,"utf-8")

    def handle_starttag(self, tag, attrs):
        if self.finished: return

        if tag == "h3" or tag == "h1":
            if not self.started:
                if self.root == "" or self.data == self.root:
                    for a in attrs:
                        if a[0] == "id":
                            self.stack.append(a[1])
                    self.started = True
            else:
                for a in attrs:
                    if a[0] == "id":
                        self.stack.append(a[1])

        if self.started and tag == "a":
            for attr in attrs:
                if attr[0] == "href":
                    self.href = attr[1]

    def handle_endtag(self, tag):
        if self.finished: return

        if self.started:
            if tag == "dl":
                self.stack.pop(-1)
                if len(self.stack) == 0:
                    self.finished = True

            elif tag == "h3" :
                if len(self.stack) > 1:
                    self.createMenu(self.stack[-2], self.data, self.stack[-1])

            if tag == "a":
                self.createItem(self.stack[-1], self.data, "Execute", "%s %s" % (self.browser, self.href))


def get_firefox_bm ():
    if os.path.isdir(home + "/.mozilla"):
        if os.path.isdir(home + "/.mozilla/firefox"):
            for f in os.listdir(home+"/.mozilla/firefox"):
                if ".default" in f:
                    if os.path.isfile(home + "/.mozilla/firefox/" + f + "/bookmarks.html"):
                        return home + "/.mozilla/firefox/" + f + "/bookmarks.html"
    return ""

def get_mozilla_bm ():
    if os.path.isdir(home + "/.mozilla/default"):
        l = os.listdir(home + "/.mozilla/default")
        if len(l) == 1:
            if os.path.isfile(home + "/.mozilla/default/" + l[0] + "/bookmarks.html"):
                return home + "/.mozilla/default/" + l[0] + "/bookmarks.html"
    return ""

def print_error(error):
    obm = obxml.ObMenu()
    obm.newPipe()
    for line in error.split("\n"):
        obm.createItem(None, line, "Execute", "true")
    obm.printXml()

if __name__ == "__main__":
    home = os.getenv("HOME")

    opt = OptionParser()
    opt.add_option("-f", "--firefox", action="store_const", const=1, dest="nav", help="Look for Firefox bookmarks")
    opt.add_option("-m", "--mozilla", action="store_const", const=2, dest="nav", help="Look for Mozilla Suite bookmarks")
    opt.add_option("-b", "--bookmarks", action="store", dest="filename", help="Especify the path to the bookmarks.html file")
    opt.add_option("-r", "--root", action="store", dest="root", help="Root folder of the bookmarks")
    opt.add_option("-n", "--navigator", action="store", dest="browser", help="Command to run the web browser.")
    (opts, args) = opt.parse_args()

    nav = 0
    if opts.nav:
        nav = opts.nav

    browser = ""
    if opts.browser:
        browser = opts.browser
    if browser == "":
        browser = "firefox"

    filename = ""
    if opts.filename:
        filename = opts.filename

    root = ""
    if opts.root:
        root = opts.root

    if filename != "":
        if not os.path.isfile(filename):
            print_error("ERROR: %s: not found" % (filename))
            sys.exit(1)
    else:
        if nav == 0:
            filename = get_firefox_bm()
            if filename == "":
                filename = get_mozilla_bm()
                if filename == "":
                    print_error("ERROR: No bookmarks found, please especify location.")
                    sys.exit(1)
        if nav == 1:
            filename = get_firefox_bm()
            if filename == "":
                print_error("ERROR: Firefox bookmarks not found, please especify location.")
                sys.exit(1)

        if nav == 2:
            filename = get_mozilla_bm()
            if filename == "":
                print_error("ERROR: Mozilla suite bookmarks not found, please especify location.")
                sys.exit(1)

    cachefile = "%s/.obmmoz.xml" % (home)
    lastopts = "%s/.obmmoz.conf" % (home)

    if os.path.isfile(lastopts):
        f = open(lastopts)
        last = eval(f.read())
        f.close()
        if last == opts and os.path.isfile(cachefile) and os.path.getmtime(filename) < os.path.getmtime(cachefile):
            cache = open(cachefile)
            print cache.read()
            cache.close()
            sys.exit()

    mp = MozParser()
    mp.init()
    mp.root = root
    mp.browser = browser
    mp.openFile(filename)
    mp.saveMenu(cachefile)

    f = open(lastopts, "w")
    f.write(str(opts))
    f.close()

    mp.printXml()
```
