### 1.应用到 Cloudflare Pages

将项目部署到 Cloudflare Pages 非常简单，而且性能通常比 GitHub Pages 更好。

**请按照以下步骤操作：**

1. **登录 Cloudflare**：打开你的 [Cloudflare 仪表板](https://dash.cloudflare.com/)。
2. **进入 Pages**：在左侧菜单中，选择 **Workers & Pages**，然后点击 **Create application**。
3. **连接到 Git**：选择 **Pages** 标签页，然后点击 **Connect to Git**。
4. **授权并选择仓库**：

   * 如果你是第一次使用，需要授权 Cloudflare 访问你的 GitHub 账户。
   * 在仓库列表中，找到并选择你的 `zimingcxt/book-1` 仓库。然后点击 **Begin setup**。
5. **设置构建和部署 (最关键的一步)**：

   * **Project name**：项目名称，可以保持默认 (`book-1`)。
   * **Production branch**：选择你的主分支（通常是 `main` 或 `master`）。
   * **Framework preset**：框架预设，**选择 `None`**。因为 HonKit 不是标准预设。
   * **Build settings**：配置构建信息。
     * **Build command** (构建命令):
       ```
       npx honkit build
       ```
     * **Build output directory** (构建输出目录):
       ```
       _book
       ```
     * **Environment variables (optional)** (环境变量 - 可选但建议):
       * 点击 **Add variable**。
       * Variable name: `NODE_VERSION`
       * Value: `18` 或 `20` (确保 Cloudflare 使用一个较新的 Node.js 版本来构建)

   你的设置界面看起来应该是这样：
6. **保存并部署**：

   * 点击 **Save and Deploy**。
   * Cloudflare 会开始从你的 GitHub 仓库拉取代码，运行你设置的构建命令 (`npx honkit build`)，然后将生成的 `_book` 目录部署到全球网络。

完成后，Cloudflare 会提供给你一个 `*.pages.dev` 的网址，那就是你的新网站地址！以后你每次向 GitHub 的 `main` 分支推送更新，Cloudflare 都会自动帮你重新构建和部署，非常方便。

### 2.快速发布

已安装`gh-pages` 工具自动化部署的情况下,只需要:

1. **确保 `gh-pages` 已安装**（我们之前的步骤已经装过，这里是确认）：
   **Bash**

   ```
   npm install gh-pages --save-dev
   ```
2. **在 `package.json` 中添加部署脚本**： 打开 `package.json` 文件，在 `"scripts"` 部分添加一行 `"deploy"`：
   **JSON**

   ```
   "scripts": {
     "serve": "honkit serve",
     "build": "honkit build",
     "deploy": "gh-pages -d _book"
   },
   ```
3. **一键部署**：现在，你只需要按顺序运行两个命令：
   **Bash**

   ```
   # 第一步：构建最新的网站文件
   npm run build

   # 第二步：将构建好的 _book 文件夹部署到 gh-pages 分支
   npm run deploy
   ```
   运行 `npm run deploy` 后，它会自动帮你处理所有 Git 操作。等待几分钟，你的 GitHub Pages 网站就会更新了。

   ### 3.插件冲突

   当前插件存在冲突,如下:


   ```Bash
   {

       "title": "我的一本书",
       "author": "zimingcxt",
       "description": "这是一本没什么用的笔记",
       "gitbook": "3.7.3",
       "plugins": [
           "-sharing",//国内用处不大,而且使页面复杂化
           "collapsible-chapters",
           "search-plus", 
           "-search",//替换为上面search-plus插件,但看起来没什么区别
           "back-to-top-button",
           "toc", //目录插件,原先的simple-page-toc莫名用不了,替换为正文内插入目录(插入方式见4.目录插入)
           "fontsettings",
           "code",
           "-splitter",//和其他共存会出现内容右移bug
           "prism" 
       ],

       "pluginsConfig": {
           "prism": {
               "css": [
                   "prismjs/themes/prism-tomorrow.css"
               ]
           }
       }
   }
   ```
   ### 4.目录插入

   插入方式,在想要的位置(一般在标题下方)输入即可:

   ```Bash
   <!-- toc -->
   ```
