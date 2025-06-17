# 第二节:教程(Windows)

> 本指南为个人备忘录，旨在记录如何使用 HonKit 和 GitHub Pages 在 Windows 系统上快速创建、部署和维护一个在线文档/书籍网站。
>
> - **先决条件**：请确保你的 Windows 系统已安装以下软件：
>   1. [**Node.js**](https://nodejs.org/en) (会自动包含 npm)
>   2. [**Git for Windows**](https://git-scm.com/download/win)
>   3. [**Visual Studio Code**](https://code.visualstudio.com/) (推荐)
> - **技术栈**：HonKit, Node.js, npm, Git, GitHub Pages
> - **作者**：zimingcxt

## 一、🚀 新项目从零到一快速部署

此部分涵盖了从初始化项目到网站上线的完整流程。假设新项目名为 `my-new-book`。

### 第1步：本地项目初始化

在你的电脑上为新项目做好准备。打开“命令提示符(CMD)”或“PowerShell”来执行以下命令。

```cmd
:: 1. 在你喜欢的位置创建一个新的项目文件夹 (例如 D:\projects)
mkdir my-new-book

:: 2. 进入该文件夹 (后续所有命令都在此文件夹内执行)
cd my-new-book

:: 3. 初始化 npm 项目，生成 package.json 文件 (-y 表示全部使用默认配置)
npm init -y

:: 4. 安装 HonKit 和部署工具 gh-pages
:: HonKit 是核心工具，gh-pages 用于一键部署到 GitHub Pages
npm install honkit gh-pages --save-dev
```

### 第2步：创建书籍的基础文件 (Windows 推荐方式)

我们推荐直接使用 VS Code 或记事本手动创建文件，这样可以避免不同命令行工具的兼容性问题。

1. 在** **`my-new-book` 文件夹中，**手动创建**一个名为** **`README.md` 的文件，并粘贴以下内容：
   **Markdown**

   ```
   # 我的新书
   ```
2. 同样，**手动创建**一个名为** **`SUMMARY.md` 的文件，并粘贴以下内容：
   **Markdown**

   ```
   # 目录

   * [前言](README.md)
   * [第一章](chapter1.md)
   ```

### 第3步：生成、预览项目

创建好以上两个文件后，回到命令行工具继续执行。

**DOS**

```
:: 1. 使用 HonKit 自动生成目录中定义的文件结构
:: HonKit 会读取 SUMMARY.md 并创建对应的 chapter1.md 文件
honkit init

:: 2. (可选) 本地预览，检查效果
:: 在浏览器打开 http://localhost:4000 查看
需要先执行: honkit serve
```

### 第4步：在** **`package.json` 中配置部署命令

此步骤与 macOS 完全相同。这是实现“一键部署”的关键。打开项目中的** **`package.json` 文件，找到** **`"scripts"`部分，添加** **`"deploy"` 命令。

**JSON**

```
// package.json

{
  "name": "my-new-book", // 这里会是你项目文件夹的名字
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    // 在这里添加 deploy 命令
    // "deploy": "gh-pages -d _book"
    // -d _book 的意思是将 _book 文件夹里的内容部署上去
    "deploy": "gh-pages -d _book",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    // 这里是你安装的开发依赖
    "gh-pages": "^6.3.0",
    "honkit": "^3.7.3" // 版本号可能不同
  }
}
```

### 第5步：在 GitHub 创建并关联远程仓库

此步骤与 macOS 完全相同。

1. 登录 GitHub，创建一个新的** ****Public** 仓库，仓库名建议与项目名一致（例如** **`my-new-book`）。
2. **不要**勾选任何初始化选项（如 README, .gitignore）。
3. 创建后，复制仓库的 HTTPS 地址（例如** **`https://github.com/zimingcxt/my-new-book.git`）。

**Bash**

```
:: 1. 初始化本地 Git 仓库
git init

:: 2. 关联到你刚刚在 GitHub 创建的远程仓库 (注意替换 URL)
git remote add origin https://github.com/zimingcxt/my-new-book.git

:: 3. 将源码推送到 GitHub 的 main 分支进行备份
:: 这一步不是部署网站，而是备份你的 Markdown 源文件
git add .
git commit -m "feat: initial project setup"
git push -u origin main
```

### 第6步：执行部署

此步骤与 macOS 完全相同。

**DOS**

```
:: 1. 首先，用 HonKit 构建静态网站文件，生成 _book 文件夹
honkit build

:: 2. 然后，执行你在 package.json 中定义的 deploy 脚本
npm run deploy
```

执行后，`gh-pages` 工具会自动创建一个** **`gh-pages` 分支，并将** **`_book` 文件夹的内容推送到这个分支上。

### 第7步：配置 GitHub Pages

此步骤与 macOS 完全相同，全程在 GitHub 网站上操作。

1. 进入你 GitHub 上的** **`my-new-book` 仓库页面。
2. 点击** **`Settings` ->** **`Pages`。
3. 在** **`Build and deployment` 下，将** **`Source` 设置为** **`Deploy from a branch`。
4. 在** **`Branch` 部分，选择** **`gh-pages` 分支，文件夹选择** **`/(root)`。
5. 点击** **`Save`。

等待几分钟后，你的新网站就可以通过** **`https://zimingcxt.github.io/my-new-book/` 访问了。

---

## 二、✍️ 日常维护：快捷添加目录和文章

此部分工作流与 macOS 完全相同。

### 流程概览

**修改目录 -> 创建文件 -> 编写内容 -> 提交 -> 部署**

### 详细步骤

**DOS**

```
:: 1. 修改目录文件 SUMMARY.md
:: 比如，我们想在第一章下增加一个子章节，并添加第二章
:: 用 VS Code 打开 SUMMARY.md，修改后内容如下：
::
:: # 目录
::
:: * [前言](README.md)
:: * [第一章：基础](chapter1.md)
::   * [第一节：核心概念](c1/section1.md)
:: * [第二章：进阶](chapter2.md)
::

:: 2. 自动创建文件
:: 保存 SUMMARY.md 后，运行 honkit init，它会自动创建 c1/section1.md 和 chapter2.md
honkit init

:: 3. 编写你的新文章
:: 用 VS Code 打开刚刚创建的 c1/section1.md 和 chapter2.md，开始写作...

:: 4. (可选) 本地预览
honkit serve

:: 5. 提交源码变更到 GitHub
:: 这是个好习惯，可以备份你的每一次修改
git add .
git commit -m "docs: add chapter 2 and section 1.1"
git push origin main

:: 6. 重新构建并部署到线上
honkit build
npm run deploy
```

完成！几分钟后，你网站上的内容就会更新。

---

## 三、⚙️ (进阶) 使用** **`book.json` 进行个性化配置

此部分与 macOS 完全相同。在项目根目录下创建一个** **`book.json` 文件，可以用来配置书名、作者、插件等。

### `book.json` 示例

**JSON**

```
// book.json

{
    // 书本的标题，会显示在网站的左上角
    "title": "我的新一代神书",

    // 作者
    "author": "zimingcxt",

    // 书本的描述
    "description": "这是一本关于...的划时代巨著",

    // 使用的 HonKit 版本，建议锁定以保证兼容性
    "gitbook": "3.7.3",

    // 插件列表
    // HonKit 默认带了一些插件，如 search, sharing, fontsettings
    // 你可以在这里添加更多插件，比如代码高亮
    "plugins": [
        "-sharing", // 负号表示禁用默认的 sharing 插件
        "prism",    // 添加 prism 插件用于代码高亮
        "prism-themes" // prism 的主题插件
    ],

    // 针对插件的详细配置
    "pluginsConfig": {
        "prism": {
            "css": [
                // 选择一个你喜欢的主题样式
                "prismjs/themes/prism-tomorrow.css"
            ]
        }
    }
}
```

### 如何使用带插件的配置

1. 在** **`book.json` 中添加插件名。
2. 使用 npm 安装插件，例如：`npm install honkit-plugin-prism prism-themes --save-dev`。
3. 重新运行** **`honkit install` (如果需要) 或直接** **`honkit build`，HonKit 会自动加载插件。
