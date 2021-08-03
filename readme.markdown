# Multilingual Experiment in Jekyll

The [basic *GitHub Pages* site](https://ranbureand.github.io/multilingual-experiment/) hosted in this repository and this README illustrate my approach to create a multilingual site in *[Jekyll](https://jekyllrb.com/ "Jekyll")*.

## Table of Contents

+ [Preface](#preface)
+ [Foreword](#foreword)
+ [Directory Structure](#directory-structure)
  + [Pages](#pages)
    + [Exceptions](#exceptions)
  + [Posts](#posts)
    + [Configuration](#configuration)
+ [Front Matter](#front-matter)
  + [Pages](#pages-1)
  + [Posts](#posts-1)
+ [Data Files](#data-files)
  + [Snippets](#snippets)
+ [Includes](#includes)
  + [header.html](#headerhtml)
    + [navigation.html](#navigationhtml)
    + [language-switch.html](#language-switchhtml)
      + [if page.layout == 'page'](#if-pagelayout--page)
      + [elsif page.layout == 'post'](#elsif-pagelayout--post)
      + [else](#else)
      + [Fallback Page](#fallback-page)
    + [title.html](#titlehtml)
  + [localizations.html](#localizationshtml)
+ [Sundries](#sundries)
  + [Multilingual Sitemap](#multilingualsitemap)
    + [Sitemap Index](#sitemap-index)
    + [Sitemaps](#sitemaps)
  + [RSS Feed](#rss-feed)
  + [404 Page Not Found](#404-page-not-found)
+ [Resources](#resources)
+ [Afterword](#afterword)

## Preface

When I found myself coding a multilingual site in [Jekyll](https://jekyllrb.com/ "Jekyll"), I stumbled on [a lot of useful resources](#resources) while surfing the Web, but I struggled not a little while trying to digest and replicate their approaches because of the lack of a concrete, working example to look at.

At first, I tried to replicate their approaches directly in the site I was working on, but this quickly backfired because it proved to be too big of a bite to chew for a designer who codes.

Not giving up, I then opted for creating a basic site from scratch, so that I could just focus on experimenting with multiple languages in Jekyll without any extra complexity in the picture.

That very same basic site is hosted in this repository, which I gladly share with the world as an example project, hoping to help anybody who is into coding a multilingual site using Jekyll.

## Foreword

A few words before starting. Sites built with the approach illustrated in this README:

+ can support [as many languages as needed](#directory-structure)
+ can serve pages or posts that do not necessarily need to be translated in all the supported languages
+ have a [language switch](#language-switchhtml) that can either direct web surfers to view the current page or post in the selected language, if available, or can direct them to an alternative [fallback page](#fallback-page)
+ do not need you to install custom plugins
+ leverage the basics of Jekyll and thus should be relatively future-proof (last famous words)
+ can be published as *GitHub Pages* sites

Specifically, [the basic site](https://ranbureand.github.io/multilingual-experiment/) hosted in this repository and used as an example:

+ is visually quite crude, since the focus is on illustrating a structural (not visual) approach to building multilingual sites
+ supports English and Italian as example languages

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

### Pages

We organize the pages into as many subdirectory as the languages that we plan to support, and name them using [ISO language codes](https://www.w3schools.com/tags/ref_language_codes.asp "HTML Language Code Reference in W3Schools"). This basic site has two subdirectories, one named `en` for grouping the English pages, and one named `it` for grouping the Italian pages.

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

#### Exceptions

But, of course, there are exceptions. We place the pages `404.html`, `index.html`, and `sitemap.html` in the root directory of the site. Why?

`404.html` and `index.html` are *unique* pages because Jekyll builds and serves automatically one and only one of them at a time.

`sitemap.xml` instead is none other than a [Sitemap index](https://www.sitemaps.org/protocol.html#index "Sitemaps XML Format, Sitemap index") which points to the other localized sitemaps in the respective language subfolders (read the section [Multilingual Sitemap](#multilingual-sitemap) for more details).

### Posts

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

#### Configuration

We then add the following configuration options in the `_config.yml` file placed in the site’s root directory:

``` yaml
defaults:
-
  scope:
    path: '_posts/en'
    type: 'posts'
  values:
    permalink: 'en/story/:title'
    language: en
-
  scope:
    path: '_posts/it'
    type: 'posts'
  values:
    permalink: 'it/storia/:title'
    language: it
```

By setting global permalinks for posts, we can reach, for example, the English post named `2021-01-01-hello-world.markdown` and the Italian post named `2021-01-01-ciao-mondo.markdown` at the URLs `www.site.ext/en/hello-world.html` and `www.site.ext/it/ciao-mondo.html`, respectively.

## Front Matter

### Pages

Here is how the front matter of a page looks like:

``` yaml
---
layout: page

title: Stories
description: Stories.

language: en
language_reference: stories

published: true
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

published: true
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

published: true
---
```

Both pages have the variable `language_reference` set to `stories` so that they can be easily related.

We can use `language` to retrieve only the pages that have the same language, and `language_reference` to retrieve only the pages that return the same content translated in different languages.

### Posts

Here is how the front matter of a post looks like:

``` yaml
---
layout: post

title: Hello World
description: Hello world.
date: '2021-01-01 00:00:00'

language: 'en'
language_reference: 'world'

published: true
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

published: true
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

published: true
---
```

Both posts have the variable `language_reference` set to `world` so that they can be easily related.

Again, we can use `language` to retrieve only the posts that have the same language, and `language_reference` to retrieve only the posts that return the same content translated in different languages.

## Data Files

### Snippets

We create a YAML [Data File](https://jekyllrb.com/docs/datafiles/ "Data Files") named `snippets.yml` to store the different translations of the user interface copy as additional data in the `_data` subdirectory.

We then create a new variable named `snippets` in the `base.html` layout to shorten the code that we need to write to access the data contained in the `snippets.yml` file:

``` liquid
{%- assign snippets = site.data.snippets %}
```

Since the `base.html` layout works as the base for all the other layouts, if we place the variable `snippets` there, we can then call it from any page.

Through this variable, we can write just `snippets.name_of_the_data_item` when accessing a data item rather than the full, longer `site.data.snippets.name_of_the_data_item`.

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

The purpose of most of the includes in this basic site is building the navigation.

### header.html

The include `header.html` generates the header in the HTML page. It, in turn, has three more includes:

+ `title.html`
+ `navigation.html`
+ `language-switch.html`

``` liquid
<header>
  {% include site-title.html %}
  <nav>
    {% include navigation.html %}

    {% include language-switch.html %}
  </nav>
</header>
```

#### navigation.html

The include `navigation.html` generates an unordered list containing all the published pages having the same `language` variable as the current page.

``` liquid
<ul>
  {%- assign navigation_pages = site.pages
    | where: 'layout', 'page'
    | where: 'language', page.language
    | where: 'published', true
    | sort: 'order' %}
  {%- for navigation_page in navigation_pages %}
  <li{%- if navigation_page.title == page.title %} class="current"{%- endif %}>
    <a href="{{ site.baseurl }}{{ navigation_page.url }}">{{ navigation_page.title }}</a>
  </li>
  {%- endfor %}
</ul>
```

In the code above, we create a new variable named `navigation_pages` which returns a list of the pages that, [in their front matter](#pages-1), have:

+ the `layout` variable set to `page`
+ the `language` variable set to the language of the current page (`page.language`)
+ the `published` variable set to `true`

and we order the list according to the `order` variable. We then loop trough the array of pages and generate the list items of the unordered list.

Whenever the title of the current page in the array (`navigation_page.title`) matches the title of the current page (`page.title`), we add a class named `current` to the corresponding `<li/>` tag.

#### language-switch.html

The include `language-switch.html` generates an unordered list containing all the languages supported in the site. You can use the list to switch to one of the other language translations of the current page/post, if available.

``` liquid
<ul>
  {%- for language in snippets.languages %}

    {%- if page.layout == 'page' %}
      {%- assign navigation_pages = site.pages
        | where: 'language_reference', page.language_reference
        | where: 'language', language[1].slug %}
      {%- if navigation_pages.size == 1 %}
        {%- for navigation_page in navigation_pages %}
          {%- assign url = site.baseurl | append: navigation_page.url %}
        {%- endfor %}
      {%- else %}
        {%- assign navigation_pages = site.pages
          | where: 'language_reference', site.fallback_page
          | where: 'language', language[1].slug %}
        {%- for navigation_page in navigation_pages %}
          {%- assign url = site.baseurl | append: navigation_page.url %}
        {%- endfor %}
      {%- endif %}

    {%- elsif page.layout == 'post' %}
      {%- assign navigation_posts = site.posts
        | where: 'language_reference', page.language_reference
        | where: 'language', language[1].slug %}
      {%- if navigation_posts.size == 1 %}
        {%- for navigation_post in navigation_posts %}
          {%- assign url = site.baseurl | append: navigation_post.url %}
        {%- endfor %}
      {%- else %}
        {%- assign navigation_pages = site.pages
          | where: 'language_reference', site.fallback_page
          | where: 'language', language[1].slug %}
        {%- for navigation_page in navigation_pages %}
          {%- assign url = site.baseurl | append: navigation_page.url %}
        {%- endfor %}
      {%- endif %}

    {%- else %}
      {%- assign navigation_pages = site.pages
        | where: 'language_reference', site.fallback_page
        | where: 'language', language[1].slug %}
      {%- for navigation_page in navigation_pages %}
        {%- assign url = site.baseurl | append: navigation_page.url %}
      {%- endfor %}

    {%- endif %}
    <li{%- if language[1].slug == page.language %} class="current"{%- endif %}>
      <a href="{{ url }}">{{ language[1].value }}</a>
    </li>
  {%- endfor %}
</ul>
```

In the code above, we loop through the languages defined in the `snippets.html` file (read the section [Snippets](#snippets) for more details).

``` yaml
languages:
  en:
    value: English
    slug: en
  it:
    value: Italian
    slug: it
```

The *for* loop contains three different code blocks that are run only if specific conditions are met. If we were to look only at its high-level structure:

``` liquid
<ul>
  {%- for language in snippets.languages %}

    {%- if page.layout == 'page' %}
      <!-- first code block -->

    {%- elsif page.layout == 'post' %}
      <!-- second code block -->

    {%- else %}
      <!-- third code block -->

    {%- endif %}
    <li {%- if language[1].slug == page.language %} class="current"{%- endif %}>
      <a href="{{ url }}">{{ language[1].value }}</a>
    </li>
  {%- endfor %}
</ul>
```

We run the first block of code only if the `layout` variable of the current page is set to `page`, else, if it is set to `post`, we run the second block of code, else, if it is set to anything else (or to nothing at all), we run the third block of code.

After at least one of the code blocks has been run, we generate the list items of the unordered list.

Whenever the slug of the current language item of the array `snippets.languages` (`language[1].slug`) matches the language of the current page (`page.language`), we add a class named `current` to the corresponding `<li/>` tag.

##### if page.layout == 'page'

``` liquid
{%- if page.layout == 'page' %}
  {%- assign navigation_pages = site.pages
    | where: 'language_reference', page.language_reference
    | where: 'language', language[1].slug %}
  {%- if navigation_pages.size == 1 %}
    {%- for navigation_page in navigation_pages %}
      {%- assign url = site.baseurl | append: navigation_page.url %}
    {%- endfor %}
  {%- else %}
    {%- assign navigation_pages = site.pages
      | where: 'language_reference', site.fallback_page
      | where: 'language', language[1].slug %}
    {%- for navigation_page in navigation_pages %}
      {%- assign url = site.baseurl | append: navigation_page.url %}
    {%- endfor %}
  {%- endif %}
```

What does the first block of code do?

``` liquid
{%- assign navigation_pages = site.pages
  | where: 'language_reference', page.language_reference
  | where: 'language', language[1].slug %}
```

We create a new variable named `navigation_pages` which returns a list of the pages that, [in their front matter](#pages-1), have:

+ the `language_reference` variable equal to the current page’s `language_reference` variable (`page.language_reference`)
+ the `language` variable equal to the slug of the current language item (`language[1].slug`) in the array `snippets.languages`

If we set the front matter of the pages correctly, the size of the array `navigation_pages` should be:

+ either equal to one if the current page <u>has</u> a corresponding page translated in the current language item of the array `snippets.languages`
+ or equal to zero if the current page <u>does not have</u> a corresponding page translated in the current language item of the array `snippets.languages`

``` liquid
{%- if navigation_pages.size == 1 %}
  {%- for navigation_page in navigation_pages %}
    {%- assign url = site.baseurl | append: navigation_page.url %}
  {%- endfor %}
```

If the size of the array `navigation_pages` is equal to one, we loop through the array `navigation_pages` and create a new variable named `url` by combining the `site.baseurl` (defined in the `_config.yml` file) and the url of the one page (`navigation_page.url`) contained in the array `navigation_pages`.

``` liquid
{%- else %}
  {%- assign navigation_pages = site.pages
    | where: 'language_reference', site.fallback_page
    | where: 'language', language[1].slug %}
  {%- for navigation_page in navigation_pages %}
    {%- assign url = site.baseurl | append: navigation_page.url %}
  {%- endfor %}
{%- endif %}
```

If instead, the size of the array `navigation_pages` is equal to zero (or more than one, which is trouble), we do not have a corresponding page in the current language item of the array `snippets.languages` to switch to.

Thus, we provide a fallback page (`site.fallback_page`) so that web surfers who interact with the language switch and press on a language that does not support the current page are at least redirected to a meaningful page in the language they selected.

We set the `fallback_page` in the `_config.yml` file placed in the site’s root directory:

``` yaml
fallback_page: 'stories'
```

The fallback pages of this basic site are those whose `language_reference` variable is set to `stories`.

Why `stories`? Because the pages whose `language_reference` variable is set to `stories` work as *home* pages, since they:

+ return a list of all the published posts (they have exactly the same structure as the `index.html` page)
+ have a translated counterpart in all the languages supported on the site

##### elsif page.layout == 'post'

``` liquid
{%- elsif page.layout == 'post' %}
  {%- assign navigation_posts = site.posts
    | where: 'language_reference', page.language_reference
    | where: 'language', language[1].slug %}
  {%- if navigation_posts.size == 1 %}
    {%- for navigation_post in navigation_posts %}
      {%- assign url = site.baseurl | append: navigation_post.url %}
    {%- endfor %}
  {%- else %}
    {%- assign navigation_pages = site.pages
      | where: 'language_reference', site.fallback_page
      | where: 'language', language[1].slug %}
    {%- for navigation_page in navigation_pages %}
      {%- assign url = site.baseurl | append: navigation_page.url %}
    {%- endfor %}
  {%- endif %}
```

The second block of code behaves akin to the first, with the only difference that we manipulate an array of posts (`navigation_posts`) rather than one of pages (`navigation_pages`).

##### else

``` liquid
{%- else %}
  {%- assign navigation_pages = site.pages
    | where: 'language_reference', site.fallback_page
    | where: 'language', language[1].slug %}
  {%- for navigation_page in navigation_pages %}
    {%- assign url = site.baseurl | append: navigation_page.url %}
  {%- endfor %}
```

The third block of code runs in the remote eventuality in which both the first and second blocks of code are not run, so that we make sure, again, to serve a fallback page to our web surfers.

##### Fallback Page

How can we be sure that the fallback page truly works?

In this basic site, not all the pages and posts are translated into all the supported languages—on purpose.

###### Pages

| English | Italian |
| - | - |
| preface.html | prefazione.html |
| stories.html | storie.html |
| postface.html| — |

If you go to [the English page *Postface*](https://ranbureand.github.io/multilingual-experiment/en/postface.html) and press on *Italian* in the language switch, you can see that you are indeed redirected to the Italian page *Storie*.

###### Posts

| English | Italian |
| - | - |
| hello-world.markdown | ciao-mondo.markdown |
| hello-mars.markdown | ciao-marte.markdown |
| — | ciao-giove.markdown |

Similarly, if you go to [the Italian post *Ciao Giove*](https://ranbureand.github.io/multilingual-experiment/it/storia/ciao-giove) and press on *English* in the language switch, you can see that you are indeed redirected to the English page *Stories*.

#### title.html

The include `title.html` generates the title of this basic site.

``` liquid
{%- if page.language == site.default_language %}
  {%- assign url = site.baseurl | append: '/'%}
{%- else %}
  {%- assign navigation_pages = site.pages
    | where: 'language_reference', site.fallback_page
    | where: 'language', page.language %}
  {%- for navigation_page in navigation_pages %}
    {%- assign url = site.baseurl | append: navigation_page.url %}
  {%- endfor %}
{%- endif %}
<h1>
  <a href="{{ url }}" {%- if page.url == '/' %} class="current"{%- endif %}>{{ site.title }}</a>
</h1>
```

Again, we have two different code blocks that are run only if specific conditions are met.

We run the first code block when the language of the current page (`page.language`) is equal to the default language (`site.default_language`) defined in the `_config.yml` file. Through it we create a new variable named `url` by combining the `site.baseurl` (defined in the `_config.yml` file) and `/`, that is, the domain name of the site. Web surfers who browse the site in the default language are directed to the main page when they press on the title.

Else, we run the second code block to provide the usual fallback page already discussed above (read the section [language-switch.html](#language-switchhtml) for more details). Web surfers who browse the site in a language different than the default one are directed to the fallback page in their current language when they press on the title.

### localizations.html

The include `localizations.html` adds `<link rel="alternate" … />` tags in the `<head/>` tag of a page [to tell search engines](https://developers.google.com/search/docs/advanced/crawling/localized-versions "Tell Google about localized versions of your page") if there are multiple versions of the page for different languages or regions.

``` liquid
{%- if page.layout == 'page' %}
  {%- assign localized_pages = site.pages
    | where: 'language_reference', page.language_reference
    | sort: 'language' %}
  {%- for localized_page in localized_pages %}
    <link rel="alternate" hreflang="{{ localized_page.language }}" href="{{ site.baseurl }}{{ localized_page.url }}" />
  {%- endfor %}

{%- elsif page.layout == 'post' %}
  {%- assign localized_posts = site.posts
  | where: 'language_reference', page.language_reference
  | sort: 'language' %}
  {%- for localized_post in localized_posts %}
    <link rel="alternate" hreflang="{{ localized_post.language }}" href="{{ site.baseurl }}{{ localized_post.url }}" />
  {%- endfor %}

{%- elsif page.layout == 'index' %}
  {%- assign localized_pages = site.pages
    | where: 'language_reference', site.fallback_page
    | sort: 'language' %}
  {%- for localized_page in localized_pages %}
    <link rel="alternate" hreflang="{{ localized_page.language }}" href="{{ site.baseurl }}{{ localized_page.url }}" />
  {%- endfor %}
{%- endif %}
```

Again, we have three different code blocks that are run only if specific conditions are met (read the section [language-switch.html](#language-switchhtml) for more details).

## Sundries

*Coming soon…*

### Multilingual Sitemap

#### Sitemap Index

The page named `sitemap.html` is placed in the root directory of the site. It is none other than a [Sitemap index](https://www.sitemaps.org/protocol.html#index "Sitemaps XML Format, Sitemap index") which points to the other localized sitemaps in the respective language subfolders.

``` liquid
---
layout: none

sitemap:
  exclude: true
---

<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">

  {%- assign pages = site.pages | where: 'title', 'Sitemap' %}

  {%- for page in pages %}
    <url>
      <loc>{{ site.absoluteurl }}{{ page.url | remove: 'index.html' }}</loc>

      {%- if page.sitemap.lastmod %}
        {%- assign lastmod = page.sitemap.lastmod | date: '%Y-%m-%d' %}
      {%- elsif page.date %}
        {%- assign lastmod = page.date | date_to_xmlschema %}
      {%- else %}
        {%- assign lastmod = site.time | date_to_xmlschema %}
      {%- endif %}
      <lastmod>{{ lastmod }}</lastmod>

      {%- if page.sitemap.changefreq %}
        {%- assign changefreq = page.sitemap.changefreq %}
      {%- else %}
        {%- assign changefreq = 'monthly' %}
      {%- endif %}
      <changefreq>{{ changefreq }}</changefreq>

      {%- if page.sitemap.priority %}
        {%- assign priority = page.sitemap.priority %}
      {%- else %}
        {%- assign priority = 0.3 %}
      {%- endif %}
      <priority>{{ priority }}</priority>
    </url>
  {%- endfor %}

</urlset>
```

``` yaml
---
…

sitemap:
  lastmod: true
  changefreq: 'monthly'
  priority: ''
---
```

#### Sitemaps

### RSS Feed

*Coming soon…*

### 404 Page Not Found

*Coming soon…*

## Resources

+ [Making Jekyll multilingual](https://sylvaindurand.org/making-jekyll-multilingual/ "Making Jekyll multilingual")
+ [Making a multilingual website with Jekyll collections](https://www.kooslooijesteijn.net/blog/multilingual-website-with-jekyll-collections "Making a multilingual website with Jekyll collections")

## Afterword

If you feel like adding something to the subject and/or you have spotted something worth fixing, please feel free to either [drop me a line](andreaburan.com/ "Andrea Buran’s Sitefolio") or [create an issue on GitHub](https://github.com/ranbureand/multilingual-experiment/issues): thoughts, critiques, suggestions are all more than welcomed.

Thank you!

