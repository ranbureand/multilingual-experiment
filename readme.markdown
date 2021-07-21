# Multilingual Jekyll

[Here](https://ranbureand.github.io/multilingual-experiment/) you can browse the site built using the example project in this repository.

## Table of Contents

+ [Introduction](#introduction)
+ [Directory Structure](#directory-structure)
+ [Pages](#pages)
  + [Exceptions](#exceptions)
+ [Posts](#posts)
+ [Snippets](#snippets)
+ [Includes](#includes)
+ [Sundries](#sundries)
  + [Multilingual Sitemap](#multilingual-sitemap)
  + [RSS Feed](#rss-feed)
+ [Resources](#resources)

## Introduction

*Coming soon…*

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

## Pages

We organize the pages into as many subdirectory as the languages that we plan to support, named using [ISO language codes](https://www.w3schools.com/tags/ref_language_codes.asp "HTML Language Code Reference in W3Schools"). This example project has two subdirectories, one named `en` for grouping the English pages, and one named `it` for grouping the Italian pages.

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

After Jekyll has built the site, we can reach, for example, the English page `stories.html` and the Italian page `storie.html` at the URLs `www.site.ext/en/stories.html` and `www.site.ext/it/storie.html`, respectively.

### Exceptions

But, of course, there are exceptions. We place the pages `404.html`, `index.html`, and `sitemap.html` in the root directory of the project. Why?

`404.html` and `index.html` are *unique* pages because Jekyll builds and serves automatically one and only one of them at a time. `sitemap.xml` instead is none other than a [Sitemap index](https://www.sitemaps.org/protocol.html#index "Sitemaps XML Format, Sitemap index") which points to the other localized sitemaps in the respective language subfolders.

## Posts

We organize the posts following a similar logic. This example project has two subdirectories in the folder named `_posts`, one named `en` for grouping the English posts, and one named `it` for grouping the Italian posts.

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

After Jekyll has built the site, we can reach, for example, the English post named `2021-01-01-hello-world.markdown` and the Italian post named `2021-01-01-ciao-mondo.markdown` at the URLs `www.site.ext/en/hello-world.html` and `www.site.ext/it/ciao-mondo.html`, respectively.

## Configuration

*Coming soon…*

## Pages

Here is how the front matter of a page looks like:

``` yaml
---
layout: page

title: Stories
description: Stories.

language: en
language_reference: stories
---
```

But for the usual variables, we set two new ones, `language` to define the language of the page, and `language_reference` to relate different translations of the same page. The logic is based on the principle articulated in Sylvain Durand’s *[Making Jekyll Multilingual](https://sylvaindurand.org/making-jekyll-multilingual/#principle "Making Jekyll
Multilingual")*.

For example, here is the front matter of the English page *Stories*:

``` yaml
---
layout: page

title: Stories
description: Stories.

language: en
language_reference: stories
---
```

and here is the front matter of its Italian counterpart:

``` yaml
---
layout: page

title: Storie
description: Storie.

language: it
language_reference: stories
---
```

Both pages have the variable `language_reference` set to `stories` so that they can be easily related.

We can use `language` to retrieve only the pages that have the same language, and `language_reference` to retrieve only the pages that return the same content translated in different languages.

## Posts

Here is how the front matter of a post looks like:

``` yaml
---
layout: post

title: Hello World
description: Hello world.
date: '2021-01-01 00:00:00'

language: 'en'
language_reference: 'world'

publish: 'yes'
---
```

Again, but for the usual variables, we set two new ones, `language` to define the language of the post, and `language_reference` to relate different translations of the same post.

For example, here is the front matter of the English post *Hello World*:

``` yaml
---
layout: post

title: Hello World
description: Hello world.
date: '2021-01-01 00:00:00'

language: 'en'
language_reference: 'world'

publish: 'yes'
---
```

and here is the front matter of its Italian counterpart:

``` yaml
---
layout: post

title: Ciao Mondo
description: Ciao Mondo.
date: '2021-01-01 00:00:00'

language: 'it'
language_reference: 'world'

publish: 'yes'
---
```

Both posts have the variable `language_reference` set to `world` so that they can be easily related.

Again, we can use `language` to retrieve only the posts that have the same language, and `language_reference` to retrieve only the posts that return the same content translated in different languages.

## Snippets

We create a YAML [Data File](https://jekyllrb.com/docs/datafiles/ "Data Files") named `snippets.yml` to store the different translations of the user interface copy as additional data in the `_data` subdirectory.

For example, the *Back to the Top* link at the bottom of the page:

``` liquid
<a href="#{{ site.data.snippets.top.[page.language] | slugify: 'latin' }}">{{ site.data.snippets.back.[page.language] }}</a>
```

uses the following variable:

``` liquid
{{ site.data.snippets.back.[page.language] }}
```

to retrieve its copy in the current selected language from the following lines in the `snippets.yml` data file:

``` yaml
back:
  en: Back to the Top
  it: Torna in Cima

top:
  en: Top
  it: Cima
```

## Includes

*Coming soon…*

## Sundries

*Coming soon…*

### Multilingual Sitemap

*Coming soon…*

### RSS Feed

*Coming soon…*

## Resources

*Coming soon…*
