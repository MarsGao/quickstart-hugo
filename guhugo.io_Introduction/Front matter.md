---
title: "Front matter"
source: "https://gohugo.io/content-management/front-matter/"
author:
published:
created: 2025-05-19
description: "Front matter is metadata (JSON, TOML, YAML) at the top of Hugo content files, controlling content details, structure, and templates."
tags:
  - "clippings"
  - "#Hugo"
  - "#FrontMatter"
  - "#Metadata"
  - "#ContentManagement"
  - "#Taxonomies"
---
# Front matter
## AI文章摘要
- Front matter provides metadata (JSON, TOML, YAML) for Hugo content.
- It includes standard fields (date, title, draft) and custom parameters.
- Defines content description, structure, relationships, and template selection.
- Supports taxonomies and cascading values to descendant pages.
---
## 概述

每个内容文件顶部的前言是元数据，它：

- 描述内容
- 增强内容
- 与其他内容建立关系
- 控制站点的已发布结构
- 确定模板选择

使用序列化格式（ [JSON、](https://www.json.org/) [TOML](https://toml.io/) 或 [YAML](https://yaml.org/) 之一）提供 front matter。Hugo 通过检查将 front matter 与页面内容分开的分隔符来确定 front matter 格式。

通过在下面的序列化格式之间切换来查看 front matter 分隔符的示例。

```toml
+++

date = 2024-02-02T04:14:54-08:00

draft = false

title = 'Example'

weight = 10

[params]

  author = 'John Smith'

+++
```

front matter 字段可以是 [布尔值](https://gohugo.io/quick-reference/glossary/#boolean) 、 [整数](https://gohugo.io/quick-reference/glossary/#integer) 、 [浮点数](https://gohugo.io/quick-reference/glossary/#float) 、 [字符串](https://gohugo.io/quick-reference/glossary/#string) 、 [数组](https://gohugo.io/quick-reference/glossary/#array) 或 [map](https://gohugo.io/quick-reference/glossary/#map) 。请注意，TOML 格式还支持未加引号的日期/时间值。

## 领域

最常见的 front matter 字段是 、 、 和 ，但您可以使用以下任何字段指定元数据。 `date` `draft` `title` `weight`

以下字段名称是保留的。例如，您无法创建名为.在键下创建自定义字段。有关详细信息，请参阅 [parameters](https://gohugo.io/content-management/front-matter/#parameters) 部分。 `type` `params`

别名

(`string array` ） 包含一个或多个别名的数组，其中每个别名都是一个相对 URL，它将浏览器重定向到当前位置。使用对象上的 [`Aliases`](https://gohugo.io/methods/page/aliases/) 方法从模板访问这些值。有关详细信息，请参阅 [aliases](https://gohugo.io/content-management/urls/#aliases) 部分。 `Page`

建

(`map` ） [构建选项](https://gohugo.io/content-management/build-options/) 的映射。

级 联

(`map` ） front matter 键的映射，其值将向下传递给页面的后代，除非被 self 或更接近的上级级联覆盖。有关详细信息，请参阅 [cascade](https://gohugo.io/content-management/front-matter/#cascade-1) 部分。

(`string` ） 与页面关联的日期，通常是创建日期。请注意，TOML 格式还支持未加引号的日期/时间值。有关示例，请参阅 [dates](https://gohugo.io/content-management/front-matter/#dates) 部分。使用对象的 [`Date`](https://gohugo.io/methods/page/date/) 方法从模板中访问此值。 `Page`

描述

(`string` ） 在概念上与页面不同，描述通常在已发布的 HTML 文件的元素内的元素中呈现。使用对象上的 [`Description`](https://gohugo.io/methods/page/description/) 方法从模板访问此值。 `summary` `meta` `head` `Page`

draft

(`bool`) Whether to disable rendering unless you pass the flag to the command. Access this value from a template using the [`Draft`](https://gohugo.io/methods/page/draft/) method on a object.`--buildDrafts` `hugo` `Page`

expiryDate

(`string`) The page expiration date. On or after the expiration date, the page will not be rendered unless you pass the flag to the command. Note that the TOML format also supports unquoted date/time values. See the [dates](https://gohugo.io/content-management/front-matter/#dates) section for examples. Access this value from a template using the [`ExpiryDate`](https://gohugo.io/methods/page/expirydate/) method on a object.`--buildExpired` `hugo` `Page`

headless

(`bool`) Applicable to [leaf bundles](https://gohugo.io/content-management/page-bundles/#leaf-bundles), whether to set the and [build options](https://gohugo.io/content-management/build-options/) to , creating a headless bundle of [page resources](https://gohugo.io/content-management/page-resources/#metadata).`render` `list` `never`

isCJKLanguage

(`bool`) Whether the content language is in the [CJK](https://gohugo.io/quick-reference/glossary/#cjk) family. This value determines how Hugo calculates word count, and affects the values returned by the [`WordCount`](https://gohugo.io/methods/page/wordcount/), [`FuzzyWordCount`](https://gohugo.io/methods/page/wordcount/), [`ReadingTime`](https://gohugo.io/methods/page/readingtime/), and [`Summary`](https://gohugo.io/methods/page/summary/) methods on a object.`Page`

keywords

(`string array`) An array of keywords, typically rendered within a element within the element of the published HTML file, or used as a [taxonomy](https://gohugo.io/quick-reference/glossary/#taxonomy) to classify content. Access these values from a template using the [`Keywords`](https://gohugo.io/methods/page/keywords/) method on a object.`meta` `head` `Page`

lastmod

(`string`) The date that the page was last modified. Note that the TOML format also supports unquoted date/time values. See the [dates](https://gohugo.io/content-management/front-matter/#dates) section for examples. Access this value from a template using the [`Lastmod`](https://gohugo.io/methods/page/date/) method on a object.`Page`

layout

(`string`) Provide a template name to [target a specific template](https://gohugo.io/templates/lookup-order/#target-a-template), overriding the default [template lookup order](https://gohugo.io/templates/lookup-order/). Set the value to the base file name of the template, excluding its extension. Access this value from a template using the [`Layout`](https://gohugo.io/methods/page/layout/) method on a object.`Page`

linkTitle

(`string`) Typically a shorter version of the . Access this value from a template using the [`LinkTitle`](https://gohugo.io/methods/page/linktitle/) method on a object.`title` `Page`

markup

(`string`) An identifier corresponding to one of the supported [content formats](https://gohugo.io/content-management/formats/#classification). If not provided, Hugo determines the content renderer based on the file extension.

menus

(`string`, , or ) If set, Hugo adds the page to the given menu or menus. See the [menus](https://gohugo.io/content-management/menus/#define-in-front-matter) page for details.`string array` `map`

modified

Alias to [lastmod](https://gohugo.io/content-management/front-matter/#lastmod).

outputs

(`string array`) The [output formats](https://gohugo.io/configuration/output-formats/) to render. See [configure outputs](https://gohugo.io/configuration/outputs/#outputs-per-page) for more information.

params

(`map`) A map of custom [page parameters](https://gohugo.io/content-management/front-matter/#parameters).

Alias to [publishDate](https://gohugo.io/content-management/front-matter/#publishdate).

publishDate

(`string`) The page publication date. Before the publication date, the page will not be rendered unless you pass the flag to the command. Note that the TOML format also supports unquoted date/time values. See the [dates](https://gohugo.io/content-management/front-matter/#dates) section for examples. Access this value from a template using the [`PublishDate`](https://gohugo.io/methods/page/publishdate/) method on a object.`--buildFuture` `hugo` `Page`

published

Alias to [publishDate](https://gohugo.io/content-management/front-matter/#publishdate).

resources

(`map array`) An array of maps to provide metadata for [page resources](https://gohugo.io/content-management/page-resources/#metadata).

sitemap

(`map`) A map of sitemap options. See the [sitemap templates](https://gohugo.io/templates/sitemap/) page for details. Access these values from a template using the [`Sitemap`](https://gohugo.io/methods/page/sitemap/) method on a object.`Page`

slug

(`string`) Overrides the last segment of the URL path. Not applicable to section pages. See the [URL management](https://gohugo.io/content-management/urls/#slug) page for details. Access this value from a template using the [`Slug`](https://gohugo.io/methods/page/slug/) method on a object.`Page`

summary

(`string`) Conceptually different than the page , the summary either summarizes the content or serves as a teaser to encourage readers to visit the page. Access this value from a template using the [`Summary`](https://gohugo.io/methods/page/summary/) method on a object.`description` `Page`

(`string`) The page title. Access this value from a template using the [`Title`](https://gohugo.io/methods/page/title/) method on a object.`Page`

translationKey

(`string`) An arbitrary value used to relate two or more translations of the same page, useful when the translated pages do not share a common path. Access this value from a template using the [`TranslationKey`](https://gohugo.io/methods/page/translationkey/) method on a object.`Page`

type

(`string`) The [content type](https://gohugo.io/quick-reference/glossary/#content-type), overriding the value derived from the top-level section in which the page resides. Access this value from a template using the [`Type`](https://gohugo.io/methods/page/type/) method on a object.`Page`

unpublishdate

Alias to [expirydate](https://gohugo.io/content-management/front-matter/#expirydate).

url

(`string`) Overrides the entire URL path. Applicable to regular pages and section pages. See the [URL management](https://gohugo.io/content-management/urls/#slug) page for details.

weight

(`int`) The page [weight](https://gohugo.io/quick-reference/glossary/#weight), used to order the page within a [page collection](https://gohugo.io/quick-reference/glossary/#page-collection). Access this value from a template using the [`Weight`](https://gohugo.io/methods/page/weight/) method on a object.`Page`

## Parameters

Specify custom page parameters under the key in front matter:`params`

```toml
+++

date = 2024-02-02T04:14:54-08:00

draft = false

title = 'Example'

weight = 10

[params]

  author = 'John Smith'

+++
```

Access these values from a template using the [`Params`](https://gohugo.io/methods/page/params/) or [`Param`](https://gohugo.io/methods/page/param/) method on a object.`Page`

Hugo provides [embedded templates](https://gohugo.io/templates/embedded/) to optionally insert meta data within the element of your rendered pages. These embedded templates expect the following front matter parameters:`head`

The embedded templates will skip a parameter if not provided in front matter, but will throw an error if the data type is unexpected.

## Taxonomies

Classify content by adding taxonomy terms to front matter. For example, with this site configuration:

```toml
[taxonomies]

  genre = 'genres'

  tag = 'tags'
```

Add taxonomy terms as shown below:

```toml
+++

date = 2024-02-02T04:14:54-08:00

draft = false

genres = ['mystery', 'romance']

tags = ['red', 'blue']

title = 'Example'

weight = 10

[params]

  author = 'John Smith'

+++
```

You can add taxonomy terms to the front matter of any these [page kinds](https://gohugo.io/quick-reference/glossary/#page-kind):

- `home`
- `page`
- `section`
- `taxonomy`
- `term`

Access taxonomy terms from a template using the [`Params`](https://gohugo.io/methods/page/params/) or [`GetTerms`](https://gohugo.io/methods/page/getterms/) method on a object. For example:`Page`

layouts/\_default/single.html

## Cascade

A [node](https://gohugo.io/quick-reference/glossary/#node) can cascade front matter values to its descendants. However, this cascading will be prevented if the descendant already defines the field, or if a closer ancestor node has already cascaded a value for that same field.

For example, to cascade a “color” parameter from the home page to all its descendants:

```toml
+++

title = 'Home'

[cascade]

  [cascade.params]

    color = 'red'

+++
```

### Target

The `target` [^1] keyword allows you to target specific pages or [environments](https://gohugo.io/quick-reference/glossary/#environment). For example, to cascade a “color” parameter from the home page only to pages within the “articles” section, including the “articles” section page itself:

```toml
+++

title = 'Home'

[cascade]

  [cascade.params]

    color = 'red'

  [cascade.target]

    path = '{/articles,/articles/**}'

+++
```

Use any combination of these keywords to target pages and/or environments:

environment

(`string`) A [glob](https://gohugo.io/quick-reference/glossary/#glob) pattern matching the build [environment](https://gohugo.io/quick-reference/glossary/#environment). For example: .`{staging,production}`

kind

(`string`) A [glob](https://gohugo.io/quick-reference/glossary/#glob) pattern matching the [page kind](https://gohugo.io/quick-reference/glossary/#page-kind). For example: .`{taxonomy,term}`

path

(`string`) A [glob](https://gohugo.io/quick-reference/glossary/#glob) pattern matching the page’s [logical path](https://gohugo.io/quick-reference/glossary/#logical-path). For example: .`{/books,/books/**}`

### Array

Define an array of cascade parameters to apply different values to different targets. For example:

```toml
+++

title = 'Home'

[[cascade]]

  [cascade.params]

    color = 'red'

  [cascade.target]

    kind = 'page'

    path = '{/books/**}'

[[cascade]]

  [cascade.params]

    color = 'blue'

  [cascade.target]

    kind = 'page'

    path = '{/films/**}'

+++
```

For multilingual sites, defining cascade values in your site configuration is often more efficient. This avoids repeating the same cascade values on the home, section, taxonomy, or term page for each language. See [details](https://gohugo.io/configuration/cascade/).

If you choose to define cascade values in front matter for a multilingual site, you must create a corresponding home, section, taxonomy, or term page for every language.

## Emacs Org Mode

If your [content format](https://gohugo.io/content-management/formats/) is [Emacs Org Mode](https://orgmode.org/), you may provide front matter using Org Mode keywords. For example:

content/example.org

```text
#+TITLE: Example

#+DATE: 2024-02-02T04:14:54-08:00

#+DRAFT: false

#+AUTHOR: John Smith

#+GENRES: mystery

#+GENRES: romance

#+TAGS: red

#+TAGS: blue

#+WEIGHT: 10
```

Note that you can also specify array elements on a single line:

content/example.org

```text
#+TAGS[]: red blue
```

## Dates

When populating a date field, whether a [custom page parameter](https://gohugo.io/content-management/front-matter/#parameters) or one of the four predefined fields ([`date`](https://gohugo.io/content-management/front-matter/#date), [`expiryDate`](https://gohugo.io/content-management/front-matter/#expirydate), [`lastmod`](https://gohugo.io/content-management/front-matter/#lastmod), [`publishDate`](https://gohugo.io/content-management/front-matter/#publishdate)), use one of these parsable formats:

| Format | Time zone |
| --- | --- |
| `2023-10-15T13:18:50-07:00` | `America/Los_Angeles` |
| `2023-10-15T13:18:50-0700` | `America/Los_Angeles` |
| `2023-10-15T13:18:50Z` | `Etc/UTC` |
| `2023-10-15T13:18:50` | Default is `Etc/UTC` |
| `2023-10-15` | Default is `Etc/UTC` |
| `15 Oct 2023` | Default is `Etc/UTC` |

The last three examples are not fully qualified, and default to the time zone.`Etc/UTC`

To override the default time zone, set the [`timeZone`](https://gohugo.io/configuration/all/#timezone) in your site configuration. The order of precedence for determining the time zone is:

1. The time zone offset in the date/time string
2. The time zone specified in your site configuration
3. The time zone `Etc/UTC`

[^1]: The alias for is deprecated and will be removed in a future release. `_target` `target`