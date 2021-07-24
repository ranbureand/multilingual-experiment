# Multilingual Experiment in Jekyll

The [basic *GitHub Pages* site](https://ranbureand.github.io/multilingual-experiment/) hosted in this repository, and its related README, illustrate my approach to create a multilingual site in *[Jekyll](https://jekyllrb.com/ "Jekyll")*.

## Table of Contents

+ [Preface](#preface)
+ [Introduction](#introduction)
+ [Directory Structure](#directory-structure)
+ [Pages](#pages)
  + [Exceptions](#exceptions)
+ [Posts](#posts)
+ [Snippets](#snippets)
+ [Includes](#includes)
  + [header.html](#header-html)
  + [localizations.html](#localizations-html)
+ [Sundries](#sundries)
  + [Multilingual Sitemap](#multilingual-sitemap)
  + [RSS Feed](#rss-feed)
+ [Resources](#resources)

## Preface

When I found myself coding a multilingual site in *[Jekyll](https://jekyllrb.com/ "Jekyll")*, I stumbled on [a lot of useful resources](#resources) while surfing the Web, but I struggled not a little while trying to digest and replicate their approaches because of the lack of a concrete, working example to look at.

At first, I tried to replicate their approaches directly in the site I was working on, but this quickly backfired because it proved to be too big of a bite to chew for a designer who codes.

Not giving up, I then opted for creating a basic site from scratch, so that I could just focus on experimenting with multiple languages in Jekyll without any extra complexity in the picture.

That very same basic site is hosted in this repository, which I gladly share with the world as an example project, hoping to help anybody who is into coding a multilingual site using Jekyll.

## Introduction

A few directions before starting:

+ the small basic site supports only two languages, English and Italian
+
+

## Directory Structure

The directory structure of this basic site looks like this:

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

We organize the pages into as many subdirectory as the languages that we plan to support, named using [ISO language codes](https://www.w3schools.com/tags/ref_language_codes.asp "HTML Language Code Reference in W3Schools"). This basic site has two subdirectories, one named `en` for grouping the English pages, and one named `it` for grouping the Italian pages.

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

But, of course, there are exceptions. We place the pages `404.html`, `index.html`, and `sitemap.html` in the root directory of the site. Why?

`404.html` and `index.html` are *unique* pages because Jekyll builds and serves automatically one and only one of them at a time. `sitemap.xml` instead is none other than a [Sitemap index](https://www.sitemaps.org/protocol.html#index "Sitemaps XML Format, Sitemap index") which points to the other localized sitemaps in the respective language subfolders.

## Posts

We organize the posts following a similar logic. This basic site has two subdirectories in the folder named `_posts`, one named `en` for grouping the English posts, and one named `it` for grouping the Italian posts.

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

We then create a new variable named `snippets` in the `base.html` layout to shorten the code that we need to write to access the data contained in the `snippets.yml` file:

``` liquid
{%- assign snippets = site.data.snippets %}
```

Through this variable, we can spare ourselves from writing `site.data.snippets.top[current_language]` and instead use the shorter form `snippets.top[current_language]`.

For example, the piece of code that generates *Back to the Top* link at the bottom of the page:

``` liquid
<a href="#{{ snippets.top[page.language] | slugify: 'latin' }}">{{ snippets.back[page.language] }}</a>
```

uses the following variable:

``` liquid
{{ snippets.back[page.language] }}
```

to retrieve the name of the link in the current selected language from the following lines in the `snippets.yml` data file:

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

### header.html

*Coming soon…*

#### Navigation

*Coming soon…*

#### Language Switch

*Coming soon…*

### localizations.html

*Coming soon…*

## Sundries

*Coming soon…*

### Multilingual Sitemap

*Coming soon…*

### RSS Feed

*Coming soon…*

## Resources

+ [Making Jekyll multilingual](https://sylvaindurand.org/making-jekyll-multilingual/ "Making Jekyll multilingual")
+ [Making a multilingual website with Jekyll collections](https://www.kooslooijesteijn.net/blog/multilingual-website-with-jekyll-collections "Making a multilingual website with Jekyll collections")
