---
title: "Quick start"
source: "https://gohugo.io/getting-started/quick-start/"
author:
published:
created: 2025-05-17
description: "快速指南：创建、添加内容、配置并发布一个基本的Hugo静态网站。"
tags:
  - "clippings"
  - "Hugo"
  - "Static Site"
  - "Tutorial"
  - "Web Development"
  - "Command Line"
---
# Quick start
## AI文章摘要
- Hugo建站快速入门：安装Hugo/Git，熟悉命令行。
- 步骤：创建站点，添加内容（Markdown, 草稿）。
- 配置站点（`hugo.toml`），使用主题。
- 命令：`hugo new site`, `hugo new content`, `hugo server`, `hugo`等。
- 本地预览及生成静态文件。
---
In this tutorial you will:
1. Create a site
2. Add content
3. Configure the site
4. Publish the site
## Prerequisites
Before you begin this tutorial you must:
1. [Install Hugo](https://gohugo.io/installation/) (extended or extended/deploy edition, v0.128.0 or later)
2. [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
You must also be comfortable working from the command line.
## Create a site
### Commands
**If you are a Windows user:**
- Do not use the Command Prompt
- Do not use Windows PowerShell
- Run these commands from [PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows) or a Linux terminal such as WSL or Git > Bash
PowerShell and Windows PowerShell [are different applications](https://learn.microsoft.com/en-us/powershell/scripting/whats-new/differences-from-windows-powershell?view=powershell-7.3).
Verify that you have installed Hugo v0.128.0 or later.
```text
hugo version
```
Run these commands to create a Hugo site with the [Ananke](https://github.com/theNewDynamic/gohugo-theme-ananke) theme. The next section provides an explanation of each command.
```text
hugo new site quickstart
cd quickstart
git init
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
echo "theme = 'ananke'" >> hugo.toml
hugo server
```
View your site at the URL displayed in your terminal. Press `Ctrl + C` to stop Hugo’s development server.
### Explanation of commands
Create the [directory structure](https://gohugo.io/getting-started/directory-structure/) for your project in the `quickstart` directory.
```text
hugo new site quickstart
```
Change the current directory to the root of your project.
```text
cd quickstart
```
Initialize an empty Git repository in the current directory.
```text
git init
```
Clone the [Ananke](https://github.com/theNewDynamic/gohugo-theme-ananke) theme into the `themes` directory, adding it to your project as a [Git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules).
```text
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
```
Append a line to the site configuration file, indicating the current theme.
```text
echo "theme = 'ananke'" >> hugo.toml
```
Start Hugo’s development server to view the site.
```text
hugo server
```
Press `Ctrl + C` to stop Hugo’s development server.
## Add content
Add a new page to your site.
```text
hugo new content content/posts/my-first-post.md
```
Hugo created the file in the `content/posts` directory. Open the file with your editor.
```text
+++
title = 'My First Post'
date = 2024-01-14T07:07:07+01:00
draft = true
+++
```
Notice the `draft` value in the [front matter](https://gohugo.io/content-management/front-matter/) is `true`. By default, Hugo does not publish draft content when you build the site. Learn more about [draft, future, and expired content](https://gohugo.io/getting-started/usage/#draft-future-and-expired-content).
Add some [Markdown](https://daringfireball.net/projects/markdown) to the body of the post, but do not change the `draft` value.
```text
+++
title = 'My First Post'
date = 2024-01-14T07:07:07+01:00
draft = true
+++
## Introduction
This is **bold** text, and this is *emphasized* text.
Visit the [Hugo](https://gohugo.io) website!
```
Save the file, then start Hugo’s development server to view the site. You can run either of the following commands to include draft content.
```text
hugo server --buildDrafts
hugo server -D
```
View your site at the URL displayed in your terminal. Keep the development server running as you continue to add and change content.
When satisfied with your new content, set the front matter `draft` parameter to `false`.
Hugo’s rendering engine conforms to the CommonMark [specification](https://spec.commonmark.org/) for Markdown. The CommonMark organization provides a useful [live testing tool](https://spec.commonmark.org/dingus/) powered by the reference implementation.
## Configure the site
With your editor, open the [site configuration](https://gohugo.io/configuration/) file (`hugo.toml`) in the root of your project.
```text
baseURL = 'https://example.org/'
languageCode = 'en-us'
title = 'My New Hugo Site'
theme = 'ananke'
```
Make the following changes:
1. Set the `baseURL` for your production site. This value must begin with the protocol and end with a slash, as shown above.
2. Set the `languageCode` to your language and region.
3. Set the `title` for your production site.
Start Hugo’s development server to see your changes, remembering to include draft content.
```text
hugo server -D
```
Most theme authors provide configuration guidelines and options. Make sure to visit your theme’s repository or documentation site for details.
[The New Dynamic](https://www.thenewdynamic.com/), authors of the Ananke theme, provide [documentation](https://github.com/theNewDynamic/gohugo-theme-ananke#readme) for configuration and usage. They also provide a [demonstration site](https://gohugo-ananke-theme-demo.netlify.app/).
## Publish the site
In this step you will *publish* your site, but you will not *deploy* it.
When you *publish* your site, Hugo creates the entire static site in the `public` directory in the root of your project. This includes the HTML files, and assets such as images, CSS files, and JavaScript files.
When you publish your site, you typically do *not* want to include [draft, future, or expired content](https://gohugo.io/getting-started/usage/#draft-future-and-expired-content). The command is simple.
```text
hugo
```
To learn how to *deploy* your site, see the [host and deploy](https://gohugo.io/host-and-deploy/) section.
## Ask for help
Hugo’s [forum](https://discourse.gohugo.io/) is an active community of users and developers who answer questions, share knowledge, and provide examples. A quick search of over 20,000 topics will often answer your question. Please be sure to read about [requesting help](https://discourse.gohugo.io/t/requesting-help/9132) before asking your first question.
## Other resources
For other resources to help you learn Hugo, including books and video tutorials, see the [external learning resources](https://gohugo.io/getting-started/external-learning-resources/) page.

# Hugo 建站快速入门概览
<mcfile name="Quick start.md" path="c:/GkDesktop/OneDrive/GkObsidian/2-部门工作/2-业务中心/gaochang网站管理/guhugo.io/Quick start.md"></mcfile> 文档主要分为四个核心步骤：**创建站点、添加内容、配置站点、发布站点**。这与您项目初期需要完成的工作是高度一致的。
## 1. 先决条件 (Prerequisites)
*   **安装 Hugo**: 文档要求 Hugo v0.128.0 或更高版本。您的项目规划中也提到了指定 Hugo 版本（例如 `Hugo >= 0.110.0`），建议使用最新的稳定版。
*   **安装 Git**: Git 用于版本控制，特别是当您使用主题（通常作为 Git 子模块添加）和未来通过 GitHub Pages 部署时，这是必需的。
*   **熟悉命令行**: Hugo 的主要操作依赖命令行。文档特别提醒 Windows 用户，推荐使用 PowerShell (不是旧的 Command Prompt 或 Windows PowerShell) 或 Linux 终端 (如 WSL, Git Bash)。这与您常用的 Windows 11 + WSL2 环境是匹配的。
## 2. 创建站点 (Create a site)
核心命令：
*   `hugo new site quickstart`: 这会在当前目录下创建一个名为 `quickstart` 的新 Hugo 项目文件夹，并生成标准的目录结构。对于您的项目，可以将 `quickstart` 替换为项目名，例如 `gaochang-hugo-site`。
    *   **项目关联**：这是您高昌官网项目的起点。
*   `cd quickstart`: 进入项目根目录。
*   `git init`: 初始化 Git 仓库。
*   `git submodule add <theme-url> themes/<theme-name>`: 添加主题。Quick Start 中以 Ananke 主题为例。
    *   **项目关联**：您的项目规划中提到“主题选型与要求”，后续您会根据需求（轻量化、多语言、产品目录等）选择合适的主题，并使用此命令或类似方式将其集成到项目中。
*   `echo "theme = 'ananke'" >> hugo.toml`: 在 Hugo 的主配置文件 `hugo.toml` (较新版本 Hugo 使用 `hugo.toml`，旧版本可能是 `config.toml`) 中指定要使用的主题。
    *   **项目关联**：选定主题后，您需要在此配置文件中声明。
*   `hugo server`: 启动 Hugo 的内置开发服务器。默认情况下，您可以在 `http://localhost:1313/` 预览站点。
    *   **项目关联**：这是您在本地进行内容编写、主题定制和页面测试的主要方式，符合您项目规划中提到的“本地 `hugo server` 浏览测试页面结构”。
## 3. 添加内容 (Add content)
核心命令：
*   `hugo new content posts/my-first-post.md`: 在 `content/posts/` 目录下创建一个名为 `my-first-post.md` 的 Markdown 文件。
    *   **项目关联**：这是您为高昌官网创建各个页面的主要方式。根据您的项目规划，您会创建产品页面、关于我们、新闻动态等。例如，创建产品页面可能是 `hugo new content products/product-a.md`。
    *   **内容目录结构**：您在项目规划中提到了详细的 `content` 目录结构方案（如按语言分子目录 `content/en/`, `content/zh/`），创建内容时路径需要遵循该规划。
*   **Front Matter**: 新创建的 Markdown 文件顶部会包含 "Front Matter"，这是一段元数据，用于定义页面的属性，如 `title`, `date`, `draft` 等。Quick Start 中示例的 Front Matter 是 TOML 格式 (由 `+++` 包围)，您的项目规划中指定使用 **YAML Frontmatter** (通常由 `---` 包围)。
    *   **项目关联**：您的项目规划中对 Front Matter 有详细要求，包括通用字段（`title`, `date`, `description`, `keywords` 等）和特定页面类型字段（如产品页面的 `product_id`, `categories`, `featured_image` 等）。您需要确保创建内容时，Front Matter 符合这些规范。
*   **草稿状态 (Draft)**: `draft = true` 意味着这个页面在默认情况下不会被构建到最终的站点中。这对于正在编写或未完成的内容很有用。
    *   `hugo server -D` 或 `hugo server --buildDrafts`: 启动开发服务器时，如果想预览草稿内容，需要加上 `-D` 或 `--buildDrafts` 参数。
    *   当内容完成后，需要将 `draft` 设置为 `false`。
*   **Markdown 内容**: Front Matter 之下就是标准的 Markdown 内容。
    *   **项目关联**：您项目的所有页面内容都将以 Markdown 格式编写。
## 4. 配置站点 (Configure the site)
*   编辑 `hugo.toml` (或 `config.toml`) 文件：
    *   `baseURL`: 您站点的最终生产环境 URL (例如，对于 GitHub Pages 可能是 `https://yourusername.github.io/your-repo/`)。
    *   `languageCode`: 站点的默认语言代码 (例如 `en-us` 代表美式英语)。
        *   **项目关联**：您的项目核心语言是英语，支持中文、德语、意大利语。Hugo 的多语言配置会在这里及更详细的语言配置块中进行。
    *   `title`: 站点的标题。
    *   `theme`: 已在创建站点步骤中添加。
    *   **项目关联**：多语言支持是您项目的核心需求。Hugo 的多语言配置通常在 `hugo.toml` 中进行，例如定义可用的语言、每种语言的 `languageName`, `weight` (用于排序), `contentDir` (如果采用子目录方式管理多语言内容，如 `content/zh`) 等。Quick Start 对此涉及较浅，但这是您项目后续配置的重点。
## 5. 发布站点 (Publish the site)
*   核心命令：`hugo`
*   这个命令会将您的整个静态站点生成到项目根目录下的 `public` 文件夹中。这个 `public` 文件夹包含了所有 HTML 文件和静态资源（图片、CSS、JS 等），可以直接部署到任何静态网站托管服务上。
    *   **项目关联**：您的项目计划使用 GitHub Pages 部署。通常，CI/CD 流程（如您规划的 `.github/workflows/gh-pages.yml`）会自动执行 `hugo` 命令，并将 `public` 目录的内容推送到 GitHub Pages 指定的分支（如 `gh-pages`）。
*   **注意**：`hugo` 命令默认不会包含 `draft = true` 的内容。
# 结合您项目的关键点回顾
*   **多语言支持**：Quick Start 本身未深入讲解多语言，但其配置站点部分提到的 `languageCode` 和内容添加部分提到的目录结构是多语言实现的基础。您项目规划中探讨的“不同语言内容放在不同子目录”或“文件名后缀”方式，以及 `translationKey` 的使用，都需要在 Hugo 配置和内容组织中体现。
*   **内容原型 (Archetypes)**：Quick Start 中使用 `hugo new content ...` 时，Hugo 会根据 `archetypes/default.md` 文件来生成新内容的初始 Front Matter 和结构。您的项目规划中提到了为产品、新闻等创建专门的 archetypes (`product.md`, `news.md` 等)，这将极大提高内容创建的效率和规范性。
*   **静态资源管理**：Quick Start 没有详细展开。您的项目规划中提到了 `/static` 目录和 Page Bundles，并希望了解其差异。
    *   `/static` 目录：这里的文件会原样复制到 `public` 目录的根路径下。适合存放全局资源，如 `robots.txt`, `favicon.ico`, 全局 CSS/JS 文件，公司 Logo 等。
    *   Page Bundles：是将与特定页面相关的资源（如文章配图）和 Markdown 文件放在同一个目录下。例如，一篇文章 `my-post.md` 和它的图片 `image1.jpg` 可以放在 `content/posts/my-post/index.md` 和 `content/posts/my-post/image1.jpg`。这样组织更利于内容和资源的聚合管理，Hugo 也能更好地处理图片优化等。对于您产品目录中的大量产品图片，Page Bundles 会是更合适的选择。
*   **主题定制**：Quick Start 使用了一个现成主题。您的项目也需要选择并可能定制主题，以满足品牌和功能需求。
* 