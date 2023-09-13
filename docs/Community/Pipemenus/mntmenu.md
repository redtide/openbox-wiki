# mntmenu

Originally appeared on `david.chalkskeletons.com/scripts/` repository.

Retrieved from the depths of the [Wayback Machine](https://web.archive.org/web/20130914080232/http://david.chalkskeletons.com/scripts/mntmenu.pl).

```perl
#!/usr/bin/perl

#Written by Matthew Fitzgibbons, 03/25/05
#Bugfixes 05/01/05

use strict;

print "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
print "<openbox_pipe_menu>\n";

if (@ARGV[0] ne "") {
    print "\t<item label=\"Mount\">\n";
    print "\t\t<action name=\"Execute\"><execute>mount @ARGV[0]</execute></action>\n";
    print "\t</item>\n";
    print "\t<item label=\"Unmount\">\n";
    print "\t\t<action name=\"Execute\"><execute>umount @ARGV[0]</execute></action>\n";
    print "\t</item>\n";
    print "</openbox_pipe_menu>\n";
    exit;
}

open FSTAB, "/etc/fstab" or die $!;

my @fstab;
my $mount;
my $label;
my $usermountable = 0;
my $i = 0;
my $j = 0;
my $name = 0;
while (<FSTAB>) {
  @fstab[$i] = $_;
  ++$i;
}

close FSTAB;

foreach $mount (@fstab) {
    #ignore empty lines
    next if (substr($mount,0,1) eq "\n");
    #remove leading whitespace
    while (substr($mount,0,1) eq " " || substr($mount,0,1) eq "\t") {
        $mount = substr($mount,1,length($mount) - 1);
    }
    #ignore comment lines
    next if (substr($mount,0,1) eq "\#");
    #find filesystems that are user mountable
    $usermountable = 1 if ($mount =~ "user");

    if ($usermountable) {
        #find position of mount point for label
        #NOTE: the split function won't compile on my machine :(
        $i = 0;
        while ((substr($mount,$i,1) ne " ") && (substr($mount,$i,1) ne "\t")) {++$i;}
        while (substr($mount,$i,1) eq " " || substr($mount,$i,1) eq "\t") {++$i;}
        $j = $i;
        while ((substr($mount,$j,1) ne " ") && (substr($mount,$j,1) ne "\t")) {++$j;}
        $label = substr($mount,$i + 1,$j - $i - 1);
        print "\t<menu id=\"mnt$name\" label=\"$label\" execute=\"perl $0 $label\" />\n";
        ++$name;
        $usermountable = 0;
    }
}

print "</openbox_pipe_menu>\n";

# mntmenu.pl: an openbox pipe menu that parses /etc/fstab for user mountable filesystems and allows the user to mount them
# Copyright (C) 2005 Matthew Fitzgibbons

# This program is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation; either version 2 of the License, or (at your option) any later version.

# This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

# You should have received a copy of the GNU General Public License along with this program; if not, write to the Free Software Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA

# you may email the author at sildan@nienna.org or visit my website at nienna.org
```
