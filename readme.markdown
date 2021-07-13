# Multilingual Jekyll

## Table of contents

+ [Directory Structure](#directory-structure)
+ [Pages](#pages)

## Directory Structure

The multilingual Jekyll site looks like this:

```
.
├── _data
│   └── snippets.yml
├── _includes
│   ├── head.html
│   ├── header.html
│   ├── localizations.html
│   └── references.html
├── _layouts
│   ├── base.html
│   ├── index.html
│   ├── page.html
│   └── post.html
├── _posts
│   ├── en
│   │   ├── YYYY-MM-DD-title.markdown
│   │   ├── …
│   │   └── YYYY-MM-DD-title.markdown
│   └── it
│       ├── YYYY-MM-DD-titolo.markdown
│       ├── …
│       └── YYYY-MM-DD-titolo.markdown
├── 404.html
├── config.yml
├── en
│   ├── drafts.html
│   ├── feed.xml
│   ├── postface.html
│   ├── preface.html
│   ├── sitemap.xml
│   └── stories.html
├── index.html
├── it
│   ├── bozze.html
│   ├── feed.xml
│   ├── prefazione.html
│   ├── sitemap.xml
│   └── storie.html
└── sitemap.xml
```

### Pages

You can organize the pages into as many subfolders as the languages that you plan to support. Name the subfolders using [ISO language codes](https://www.w3schools.com/tags/ref_language_codes.asp "HTML Language Code Reference in W3Schools").

In this example project, I created two subfolders, one named `en` for grouping the English pages, and one named `it` for grouping the Italian pages.

```
│
├── en
│   ├── drafts.html
│   ├── feed.xml
│   ├── postface.html
│   ├── preface.html
│   ├── sitemap.xml
│   └── stories.html
├── it
│   ├── bozze.html
│   ├── feed.xml
│   ├── prefazione.html
│   ├── sitemap.xml
│   └── storie.html
│
```

When Jekyll builds the site, you can reach the pages at the following URLs:

```www.site.ext/en/stories.html```

```www.site.ext/it/storie.html```

### Posts

## Configuration

## Pages

### Front Matter

## Posts

### Front Matter

## Snippets

## Includes

## Sundries

### Multilingual Sitemap

### RSS Feed

## References
