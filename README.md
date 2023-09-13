# Openbox Wiki Documentation Backup

> [!WARNING]
> WIP, might be subject to force push, in which case use:
>
> ```sh
> git fetch origin
> git reset --hard origin/master
> ```

Content exported to XML from MediaWiki export page at openbox.org,
converted to Markdown and served using [Material] for [MKDocs].

## Dependencies

- python
- poetry
- mkdocs-material
- mkdocs-glightbox

## Setup

To view the site locally:

```
poetry run mkdocs serve
```

The site should be available at <http://127.0.0.1:8000>

## TODO

- Align text on the right of the images where needed
- Check for 404 links
- DesignDocuments/Actions.md, Help/Menus.md, Help/Theme.md and Help/Theme_fr.md


[Material]: https://github.com/squidfunk/mkdocs-material
[MKDocs]:   https://www.mkdocs.org
