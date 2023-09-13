# obreboot

OpenBox Reboot (pipe)Menu.

- setup your `grub` bootmenu with "default saved" (see info `grub` for more information)
- make sure you can run the `reboot` and `grub-set-default` commands.
- paste this into a file called `obreboot.pl` and add it as a pipemenu to your `menu.xml`
- You can now reboot to the boot-option of your choice with a pipe menu!

```perl
#!/usr/bin/perl
#
# OpenBox Reboot Menu (C) Biffidus 2008
#
# (only kidding, it's not copyrighted. Do whatever you like with it)
#
# This pipe menu creates a menu allowing the user to select a grub
# menu item to reboot to. In order for it to work:
#
# 1. The user must be able to run the commands reboot and grub-set-default
# 2. Grub must be configured to with the "default saved" directive.
#

$REBOOT_CMD="/usr/bin/sudo /sbin/reboot";
$SELECT_CMD="/usr/bin/sudo /sbin/grub-set-default";
$GRUB_CONFIG="/boot/grub/grub.conf";

######################################################### Parse Grub Config ###

my @entries;

open (GRUB, $GRUB_CONFIG) || do
{
    print qq|<openbox_pipe_menu><item label="Error!" /></openbox_pipe_menu>\n|;
    die "could not open $GRUB_CONFIG";
};
while (<GRUB>)
{
    chomp;
    if (/^\s*title\s+(.*)/)
    {
        push @entries, $1;
    }
}
close GRUB;

############################################################# Generate Menu ###

print "<openbox_pipe_menu>\n";

foreach ($i = 0; $i < $#entries; $i++)
{
    my $entry = $entries[$i];
    print qq| <item label="$entry">
  <action name="Execute">
    <execute>
    $SELECT_CMD $i
    </execute>
  </action>
  <action name="Execute">
    <execute>
    $REBOOT_CMD
    </execute>
  </action>
  </item>
|;
}
print "</openbox_pipe_menu>\n";

###############################################################################
```
