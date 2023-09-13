# Contribute

## Translations

![Translate-72.png][5]

Help translate Openbox! Any improvements to existing translations, or
translations to new languages would be greatly appreciated by your
fellow users.

Translations are done through "po" files. The easiest way to edit these
files is to use [Lokalize][8], which is a part of KDE (in the kdesdk package).

If you want to update an existing translation, [browse through][9]
our latest translations. You can download and modify the translation from there
(right click on the "raw" link and select "save as" or the equivalent).

If you want to create a new translation from scratch, download the current
[translation template for Openbox][10] or the [translation template for ObConf][11]
and add your translations to it. Download the file and run the command
`msginit --locale LL_CC` where LL_CC is the appropriate code for your
language. For example ru for Russian, sv for swedish or en_CA for the
Canadian variant of English. If you don't have the msginit command, you
can save the file directly as `LL_CC.po` and fill in the header
yourself, using an existing translation as a template.

When you've completed a new translation, you can submit it to the
bugzilla to have it included in the next release. To submit a
translation, follow the link below and fill out the template to create a
bug report. After the bug report has been created, attach your new "po"
file to the bug. If you for some reason don't want to use bugzilla, you
can also try to send the translation to the mailing list or contact us
directly on IRC but these methods are less reliable and the translation
might get lost.

![Important.png][3] Please make sure to specify the character encoding properly
or Openbox won't be able to read the strings, UTF-8 is preferable.

If you have any questions about what the english text means,
or anything else is unclear, please don't hesitate to contact us via the
[mailing list or on IRC][6].

Thank you for your help!

[Browse existing translations for Openbox][12]<br />
[See how many strings are translated for a language in Openbox][13]<br />
[Browse existing translations for ObConf][14]<br />
[Submit a new or updated translation][15]

(Note: use the "attach a file" button, don't paste the whole file in the comment box)

## Bug reports

![Bug-72.png][1]<br />
![Important.png][3] When submitting a bug report,
please make sure to explain to the developers how to reproduce your problem.
If we can't reproduce it, we probably can't fix it.<br />
[Browse existing bug reports][16]<br />
[Submit a new bug report][17]

## Feature requests

![Lightbulb-72.png][4]<br />
[Browse existing feature requests][18]<br />
[Submit a new feature request][19]

## Writing code

![Development-72.png][2]<br />
Openbox development is done using git. See the [Help/UsingGit][7]
page for details on how to check out the latest code
and send your changes back upstream.<br />
[Browse the Openbox git repo on GitHub.com][20]


[1]:  assets/img/Bug-72.png
[2]:  assets/img/Development-72.png
[3]:  assets/img/Important.png
[4]:  assets/img/Lightbulb-72.png
[5]:  assets/img/Translate-72.png
[6]:  Community/Portal.md
[7]:  Help/UsingGit.md
[8]:  https://userbase.kde.org/Lokalize
[9]:  https://git.icculus.org/?p=mikachu/openbox.git;a=tree;f=po;hb=backport
[10]: https://git.icculus.org/?p=mikachu/openbox.git;a=blob_plain;f=po/openbox.pot;hb=backport
[11]: https://git.icculus.org/?p=dana/obconf.git;a=blob_plain;f=po/obconf.pot;hb=HEAD
[12]: https://git.icculus.org/?p=mikachu/openbox.git;a=tree;f=po;hb=work
[13]: https://mika.l3ib.org/ob_translation_status
[14]: https://git.icculus.org/?p=dana/obconf.git;a=tree;f=po;hb=HEAD
[15]: https://bugzilla.icculus.org/enter_bug.cgi?product=Openbox&component=Translations&form_name=enter_bug
[16]: https://bugzilla.icculus.org/buglist.cgi?product=Openbox&bug_status=UNCONFIRMED&bug_status=NEW&bug_status=ASSIGNED&bug_status=REOPENED&bug_severity=blocker&bug_severity=critical&bug_severity=major&bug_severity=normal&bug_severity=minor&bug_severity=trivial&bug_severity=upstream+issue
[17]: https://bugzilla.icculus.org/enter_bug.cgi?product=Openbox&component=general&form_name=enter_bug
[18]: https://bugzilla.icculus.org/buglist.cgi?product=Openbox&bug_status=UNCONFIRMED&bug_status=NEW&bug_status=ASSIGNED&bug_status=REOPENED&bug_severity=enhancement
[19]: https://bugzilla.icculus.org/enter_bug.cgi?product=Openbox&component=general&bug_severity=enhancement&form_name=enter_bug
[20]: https://github.com/mikachu/openbox/
