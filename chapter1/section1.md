# 第一节：基本概念

## HonKit 部署 GitHub Pages 的基本概念

使用 HonKit 将你的文档或书籍部署到 GitHub Pages 是一种非常流行且有效的方式，因为它能让你免费托管你的内容，并与版本控制系统 GitHub 紧密集成。

### 1. HonKit 是什么？

HonKit 是一个**静态网站生成器**，特别适用于创建文档、技术书籍和在线手册。它的核心功能是将用 **Markdown** 语言编写的内容文件，转换为结构清晰、易于导航的静态 HTML 网站。你可以把它想象成一个“Markdown 编译器”，帮你把零散的 Markdown 文件组织成一个漂亮的网站。

### 2. GitHub Pages 是什么？

GitHub Pages 是 GitHub 提供的一项免费服务，允许你直接从 GitHub 仓库托管**静态网站**。这意味着你无需购买域名或租赁服务器，就可以把你的 HTML、CSS 和 JavaScript 文件部署到互联网上。

GitHub Pages 主要有两种类型：

* **用户/组织页面 (User/Organization Pages)：** 针对个人用户或组织的唯一网站，仓库名必须是 `你的用户名.github.io`（例如 `yourname.github.io`）。访问地址通常是 `https://yourname.github.io`。每个用户或组织**只能有一个**这样的页面。
* **项目页面 (Project Pages)：** 针对 GitHub 上的某个具体项目。仓库名可以是任意的（例如 `my-project`）。访问地址通常是 `https://yourname.github.io/my-project`。你可以为**每个项目**都创建一个项目页面。

### 3. HonKit 如何与 GitHub Pages 协同工作？

HonKit 和 GitHub Pages 的结合，可以概括为以下几个步骤：

1. **Markdown 内容创建：** 你在本地使用 Markdown 语法编写你的文档或书籍内容。所有内容都存储在你的 HonKit 项目文件夹中（例如 `README.md`、`chapter1.md` 等）。
2. **HonKit 构建网站：** 当你运行 `honkit build` 命令时，HonKit 会读取你的 Markdown 文件和 `book.json` 配置（包括目录结构 `SUMMARY.md`、插件等），然后将它们**编译生成一系列静态 HTML、CSS 和 JavaScript 文件**。这些生成的文件会存储在一个名为 `_book` 的文件夹中。
3. **Git 版本控制：** 你的 HonKit 项目（包括 Markdown 源文件、`book.json`、`_book` 文件夹等）通过 Git 进行版本控制。
4. **推送到 GitHub 仓库：** 你将本地的 HonKit 项目（特别是 `_book` 文件夹中的内容）推送到你的 GitHub 仓库。
5. **GitHub Pages 托管：** 在 GitHub 仓库的 **"Settings" -> "Pages"** 中，你将 GitHub Pages 的来源设置为包含你网站内容的特定分支和目录（通常是 `main` 分支的 `/root` 目录，因为 `_book` 文件夹就是网站的根目录）。GitHub Pages 收到这些文件后，就会将其托管，并通过一个公共 URL 提供访问。

### 4. 核心工作流程

部署一个 HonKit 网站到 GitHub Pages 的基本流程如下：

1. **本地 HonKit 项目：**

   * `honkit init`：初始化项目，生成 `README.md` 和 `SUMMARY.md`。
   * 编写 Markdown 内容。
   * 配置 `book.json`（主题、插件、元数据等）。
   * `npm install`：安装 `book.json` 中配置的任何插件。
   * `honkit serve`：本地预览你的网站。
   * `honkit build`：生成最终的静态网站文件，它们会放在 `_book` 文件夹中。
2. **Git & GitHub 仓库：**

   * 在 GitHub 上创建一个新的仓库（例如 `yourname.github.io` 用于用户页面，或 `my-project-docs` 用于项目页面）。
   * 将你的 HonKit 项目（包括 `_book` 文件夹）初始化为 Git 仓库并推送到 GitHub。
     ```bash
     git init
     git add .
     git commit -m "First HonKit build"
     git branch -M main # 确保分支名为 main 或 master
     git remote add origin https://github.com/你的用户名/你的仓库名.git
     git push -u origin main
     ```
3. **配置 GitHub Pages：**

   * 访问你的 GitHub 仓库页面。
   * 点击 **Settings (设置)**。
   * 在左侧菜单中选择 **Pages (页面)**。
   * 在 **Source (来源)** 部分，选择你的内容所在的分支（通常是 `main` 或 `master`），然后选择该分支的根目录 (`/root`) 作为部署来源。
   * 点击 **Save (保存)**。

稍等片刻，GitHub Pages 就会部署你的网站，并通过生成的 URL 提供访问。

---
