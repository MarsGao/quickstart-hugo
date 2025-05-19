---
title: "Host on GitHub Pages"
source: "https://gohugo.io/host-and-deploy/host-on-github-pages/#customize-the-workflow"
author:
published:
created: 2025-05-20
description: "本文详细介绍了如何使用GitHub Actions将Hugo静态网站部署到GitHub Pages，包括仓库设置、工作流配置及部署流程。"
tags:
  - "clippings"
  - "Hugo"
  - "GitHub Pages"
  - "GitHub Actions"
  - "网站部署"
  - "CI/CD"
---
# Host on GitHub Pages
## AI文章摘要
- 准备Hugo站点、Git和GitHub账户。
- 创建GitHub仓库，推送本地代码。
- 在GitHub Pages设置中将Source改为GitHub Actions。
- 创建`.github/workflows/hugo.yaml`文件并粘贴提供的Actions配置。
- 提交并推送更改，GitHub Actions将自动构建并部署网站。
---
## Prerequisites
Please complete the following tasks before continuing:
1. [Create a GitHub account](https://github.com/signup)
2. [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
3. [Create a Hugo site](https://gohugo.io/getting-started/quick-start/) and test it locally with `hugo server`.
## Types of sites
There are three types of GitHub Pages sites: project, user, and organization. Project sites are connected to a specific project hosted on GitHub. User and organization sites are connected to a specific account on GitHub.com.
See the [GitHub Pages documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#types-of-github-pages-sites) to understand the requirements for repository ownership and naming.

### 关于私有仓库
私有仓库（Private Repository）完全支持 GitHub Pages 功能，但需要注意以下几点：

1. **免费账户限制**：
   - GitHub 免费账户可以创建无限个私有仓库
   - 私有仓库的 GitHub Pages 功能需要 GitHub Pro 或更高级别的付费计划

2. **付费账户权益**：
   - GitHub Pro 用户可以在私有仓库中启用 GitHub Pages
   - 支持自定义域名
   - 包含更多构建时间和存储空间

3. **安全考虑**：
   - 即使仓库是私有的，发布的 GitHub Pages 网站依然是公开访问的
   - 确保不要在源码中包含敏感信息
   - 建议使用环境变量存储密钥和配置信息

### .gitignore 配置指南
Hugo 项目的 .gitignore 文件推荐配置如下：

```text
# Hugo 默认生成的目录
/public/
/resources/_gen/
/assets/jsconfig.json
/.hugo_build.lock

# 主题目录（如果主题以 git submodule 方式管理）
#themes/

# 本地开发时的缓存文件
.DS_Store
Thumbs.db

# Hugo 环境文件
.env
.env.*

# IDE 和编辑器文件
.idea/
.vscode/
*.swp
*.swo

# Node.js 依赖（如果使用了 Node.js 工具）
node_modules/
package-lock.json

# 临时文件
tmp/
temp/

# 如果使用了 Sass
.sass-cache/
*.css.map

# 本地测试文件
exampleSite/
```

**配置说明**：
1. `/public/`：Hugo 生成的静态文件，不需要版本控制
2. `/resources/_gen/`：Hugo 的缓存文件
3. `themes/`：如果主题以 git submodule 方式管理，则不要忽略
4. 根据实际开发环境添加其他规则（如 IDE 配置文件）

**最佳实践**：
- 定期检查 .gitignore 是否覆盖所有临时文件
- 使用 `git status` 确认没有不必要的文件被追踪
- 可以使用 `git check-ignore` 命令测试文件是否被忽略
## Procedure
### Step 1
Create a GitHub repository.
### Step 2
Push your local repository to GitHub.
### Step 3
Visit your GitHub repository. From the main menu choose **Settings**  >  **Pages**. In the center of your screen you will see this:
![screen capture](https://gohugo.io/host-and-deploy/host-on-github-pages/gh-pages-1.png)
### Step 4
Change the **Source** to `GitHub Actions`. The change is immediate; you do not have to press a Save button.
![screen capture](https://gohugo.io/host-and-deploy/host-on-github-pages/gh-pages-2.png)
### Step 5
In your site configuration, change the location of the image cache to the [`cacheDir`](https://gohugo.io/configuration/all/#cachedir) as shown below:
```yaml
caches:
  images:
    dir: :cacheDir/images
```
See [configure file caches](https://gohugo.io/configuration/caches/) for more information.
### Step 6
Create a file named `hugo.yaml` in a directory named `.github/workflows`.
```text
mkdir -p .github/workflows
touch .github/workflows/hugo.yaml
```
### Step 7
The workflow below ensures Hugo’s `cacheDir` is persistent, preserving modules, processed images, and [`resources.GetRemote`](https://gohugo.io/functions/resources/getremote/) data between builds.
Copy and paste the YAML below into the file you created. Change the branch name and Hugo version as needed.
.github/workflows/hugo.yaml
```yaml
# Sample workflow for building and deploying a Hugo site to GitHub Pages
name: Deploy Hugo site to Pages
on:
  # Runs on pushes targeting the default branch
  push:
    branches:
      - main
  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:
# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write
# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false
# Default to bash
defaults:
  run:
    shell: bash
jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.147.2
      HUGO_ENVIRONMENT: production
      TZ: America/Los_Angeles
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
          && sudo dpkg -i ${{ runner.temp }}/hugo.deb
      - name: Install Dart Sass
        run: sudo snap install dart-sass
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive
          fetch-depth: 0
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5
      - name: Install Node.js dependencies
        run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"
      - name: Cache Restore
        id: cache-restore
        uses: actions/cache/restore@v4
        with:
          path: |
            ${{ runner.temp }}/hugo_cache
          key: hugo-${{ github.run_id }}
          restore-keys:
            hugo-
      - name: Configure Git
        run: git config core.quotepath false
      - name: Build with Hugo
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/" \
            --cacheDir "${{ runner.temp }}/hugo_cache"
      - name: Cache Save
        id: cache-save
        uses: actions/cache/save@v4
        with:
          path: |
            ${{ runner.temp }}/hugo_cache
          key: ${{ steps.cache-restore.outputs.cache-primary-key }}
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public
  # Deployment job
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```
### Step 8
Commit and push the change to your GitHub repository.
```sh
git add -A
git commit -m "Create hugo.yaml"
git push
```
### Step 9
From GitHub’s main menu, choose **Actions**. You will see something like this:
![screen capture](https://gohugo.io/host-and-deploy/host-on-github-pages/gh-pages-3.png)
### Step 10
When GitHub has finished building and deploying your site, the color of the status indicator will change to green.
![screen capture](https://gohugo.io/host-and-deploy/host-on-github-pages/gh-pages-4.png)
### Step 11
Click on the commit message as shown above. You will see this:
![screen capture](https://gohugo.io/host-and-deploy/host-on-github-pages/gh-pages-5.png)
Under the deploy step, you will see a link to your live site.
In the future, whenever you push a change from your local repository, GitHub will rebuild your site and deploy the changes.
## Customize the workflow
The example workflow above includes this step, which typically takes 10‑15 seconds:
```yaml
- name: Install Dart Sass
  run: sudo snap install dart-sass
```
You may remove this step if your site, themes, and modules do not transpile Sass to CSS using the [Dart Sass](https://gohugo.io/functions/css/sass/#dart-sass) transpiler.
## Other resources
- [Learn more about GitHub Actions](https://docs.github.com/en/actions)
- [Caching dependencies to speed up workflows](https://docs.github.com/en/actions/using-workflows/caching-dependencies-to-speed-up-workflows)
- [Manage a custom domain for your GitHub Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages)

