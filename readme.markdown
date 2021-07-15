# Multilingual Jekyll

[Here](https://ranbureand.github.io/multilingual-experiment/) you can see the site in action.

## Table of contents

+ [Directory Structure](#directory-structure)
+ [Pages](#pages)

## Directory Structure

The directory structure of this example project looks like this:

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
├── …
├── en
│   ├── drafts.html
│   ├── feed.xml
│   ├── postface.html
│   ├── preface.html
│   ├── sitemap.xml
│   └── stories.html
├── …
├── it
│   ├── bozze.html
│   ├── feed.xml
│   ├── prefazione.html
│   ├── sitemap.xml
│   └── storie.html
├── …
```

When Jekyll builds the site, you can then reach the English page `stories.html` and the Italian page `storie.html`, for example, at the following URLs: `www.site.ext/en/stories.html` and `www.site.ext/it/storie.html`,  respectively.

### Posts

You can organize the posts following a similar logic.

In this example project, I created two subfolders in the folder named `_posts`, one named `en` for grouping the English posts, and one named `it` for grouping the Italian posts.

```
├── …
├── _posts
│   ├── en
│   │   ├── YYYY-MM-DD-title.markdown
│   │   ├── …
│   │   └── YYYY-MM-DD-title.markdown
│   └── it
│       ├── YYYY-MM-DD-titolo.markdown
│       ├── …
│       └── YYYY-MM-DD-titolo.markdown
├── …
```

When Jekyll builds the site, you can then reach the English post named `2021-01-01-hello-world.markdown` and the Italian post named `2021-01-01-ciao-mondo.markdown`, for example, at the following URLs: `www.site.ext/en/hello-world.html` and `www.site.ext/it/ciao-mondo.html`,  respectively.


## Configuration

## Pages

``` yaml
---
layout: page

title: Postface
description: Postface.

language: en
language_reference: postface
---
```

### Front Matter

## Posts

### Front Matter

## Snippets

## Includes

## Sundries

### Multilingual Sitemap

### RSS Feed

## References
