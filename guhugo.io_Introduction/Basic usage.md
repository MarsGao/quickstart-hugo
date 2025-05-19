---
title: "Basic usage"
source: "https://gohugo.io/getting-started/usage/#draft-future-and-expired-content"
author:
published:
created: 2025-05-19
description: "Learn to test, build, develop (`hugo server` with LiveReload), and deploy your Hugo site using key commands."
tags:
  - "clippings"
  - "Hugo"
  - "Site Building"
  - "Web Development"
  - "Hugo Server"
  - "Deployment"
---
# Basic usage
## AI文章摘要
- Test Hugo installation (`hugo version`) & view commands (`hugo help`).
- Build your site (`hugo`) to the `public` directory; clear `public` before building for clean output.
- Use `hugo server` for local development with live reloading.
- Manage draft, future, and expired content via command flags (`-D`, `-E`, `-F`).
- Deploy by copying the contents of the `public` directory.
---
## Test your installation

After [installing](https://gohugo.io/installation/) Hugo, test your installation by running:

```sh
hugo version
```

You should see something like:

```text
hugo v0.123.0-3c8a4713908e48e6523f058ca126710397aa4ed5+extended linux/amd64 BuildDate=2024-02-19T16:32:38Z VendorInfo=gohugoio
```

## Display available commands

To see a list of the available commands and flags:

```sh
hugo help
```

To get help with a subcommand, use the `--help` flag. For example:

```sh
hugo server --help
```

## Build your site

To build your site, `cd` into your project directory and run:

```sh
hugo
```

The [`hugo`](https://gohugo.io/commands/hugo/) command builds your site, publishing the files to the `public` directory. To publish your site to a different directory, use the [`--destination`](https://gohugo.io/commands/hugo/#options) flag or set [`publishDir`](https://gohugo.io/configuration/all/#publishdir) in your site configuration.

Hugo does not clear the `public` directory before building your site. Existing files are overwritten, but not deleted. This behavior is intentional to prevent the inadvertent removal of files that you may have added to the `public` directory after the build.

Depending on your needs, you may wish to manually clear the contents of the `public` directory before every build.

## Draft, future, and expired content

Hugo allows you to set `draft`, `date`, `publishDate`, and `expiryDate` in the [front matter](https://gohugo.io/content-management/front-matter/) of your content. By default, Hugo will not publish content when:

- The `draft` value is `true`
- The `date` is in the future
- The `publishDate` is in the future
- The `expiryDate` is in the past

Hugo publishes descendants of draft, future, and expired [node](https://gohugo.io/quick-reference/glossary/#node) pages. To prevent publication of these descendants, use the [`cascade`](https://gohugo.io/content-management/front-matter/#cascade) front matter field to cascade [build options](https://gohugo.io/content-management/build-options/) to the descendant pages.

You can override the default behavior when running `hugo` or `hugo server` with command line flags:

```sh
hugo --buildDrafts    # or -D

hugo --buildExpired   # or -E

hugo --buildFuture    # or -F
```

Although you can also set these values in your site configuration, it can lead to unwanted results unless all content authors are aware of, and understand, the settings.

As noted above, Hugo does not clear the `public` directory before building your site. Depending on the *current* evaluation of the four conditions above, after the build your `public` directory may contain extraneous files from a previous build.

A common practice is to manually clear the contents of the `public` directory before each build to remove draft, expired, and future content.

## Develop and test your site

To view your site while developing layouts or creating content, `cd` into your project directory and run:

```sh
hugo server
```

The [`hugo server`](https://gohugo.io/commands/hugo_server/) command builds your site and serves your pages using a minimal HTTP server. When you run `hugo server` it will display the URL of your local site:

```text
Web Server is available at http://localhost:1313/
```

While the server is running, it watches your project directory for changes to assets, configuration, content, data, layouts, translations, and static files. When it detects a change, the server rebuilds your site and refreshes your browser using [LiveReload](https://github.com/livereload/livereload-js).

Most Hugo builds are so fast that you may not notice the change unless you are looking directly at your browser.

### LiveReload

While the server is running, Hugo injects JavaScript into the generated HTML pages. The LiveReload script creates a connection from the browser to the server via web sockets. You do not need to install any software or browser plugins, nor is any configuration required.

### Automatic redirection

When editing content, if you want your browser to automatically redirect to the page you last modified, run:

## Deploy your site

As noted above, Hugo does not clear the `public` directory before building your site. Manually clear the contents of the `public` directory before each build to remove draft, expired, and future content.

When you are ready to deploy your site, run:

```sh
hugo
```

This builds your site, publishing the files to the `public` directory. The directory structure will look something like this:

```text
public/

├── categories/

│   ├── index.html

│   └── index.xml  <-- RSS feed for this section

├── posts/

│   ├── my-first-post/

│   │   └── index.html

│   ├── index.html

│   └── index.xml  <-- RSS feed for this section

├── tags/

│   ├── index.html

│   └── index.xml  <-- RSS feed for this section

├── index.html

├── index.xml      <-- RSS feed for the site

└── sitemap.xml
```

In a simple hosting environment, where you typically `ftp`, `rsync`, or `scp` your files to the root of a virtual host, the contents of the `public` directory are all that you need.

Most of our users deploy their sites using a [CI/CD](https://gohugo.io/quick-reference/glossary/#cicd) workflow, where a push [^1] to their GitHub or GitLab repository triggers a build and deployment. Popular providers include [AWS Amplify](https://aws.amazon.com/amplify/), [CloudCannon](https://cloudcannon.com/), [Cloudflare Pages](https://pages.cloudflare.com/), [GitHub Pages](https://pages.github.com/), [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/), and [Netlify](https://www.netlify.com/).

Learn more in the [host and deploy](https://gohugo.io/host-and-deploy/) section.

[^1]: The Git repository contains the entire project directory, typically excluding the `public` directory because the site is built *after* the push.