# MediaWiki pages XML export

## Requirements

- php
- composer
- [pandoc]
- [mediawiki-to-gfm]

## Procedure

- Go to <http://openbox.org/wiki/Special:Export>
- The options should be already set as needed:
  - [x] Include only the current revision, not the full history
  - [ ] Include templates
  - [x] Save as file
- Copy `pagelist.txt` content in the large text area and push the `Export` button
- Open the XML file as text and search for `<title>ObConf:About</title>`,
  under the line `== Screenshots ==` remove the initial part of the lines below,
  keeping only the `[[Image:<name>|thumb|<comment>]]` bits to avoid a conversion error.
- Convert the resulting XML content to markdown by using mediawiki-to-gfm:
```bash
git clone https://github.com/outofcontrol/mediawiki-to-gfm.git
cd mediawiki-to-gfm
composer update --no-dev
./convert.php --filename=/path/to/exported/file.xml
```

The default `output` directory and `gfm` format options are fine:
using `markdown_strict` [pandoc] option will only make the result worse,
by adding unnecessary whitespaces in lists, otherwise it's quite the same
as using `gfm` ([Github Flavored Markdown]).


[mediawiki-to-gfm]:         https://github.com/outofcontrol/mediawiki-to-gfm/
[Pandoc]:                   https://pandoc.org
[Github Flavored Markdown]: https://github.github.com/gfm/
