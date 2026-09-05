# 胡浩楠的个人简历

## 背景

Java 后端开发个人简历网站，展示专业能力、工作经历、项目经历和教育荣誉。内容整理自个人简历，不包含证件照或原 PDF 附件。

## 整体架构

原生 HTML + CSS，无 JavaScript、后端服务、第三方字体或构建依赖。GitHub Pages 与 Cloudflare Pages 均直接发布 `docs` 目录。

- `docs/index.html`：简历内容、站内导航和联系方式。
- `docs/assets/style.css`：桌面、手机和 A4 打印样式。
- `docs/.nojekyll`：让 GitHub Pages 直接发布静态文件。

## 详细设计

### 本地预览

在仓库根目录运行（需要 Python 3）：

```bash
python3 -m http.server 4173 --bind 127.0.0.1 --directory docs
```

打开 <http://127.0.0.1:4173/>，按 `Ctrl+C` 停止服务。也可直接用浏览器打开 `docs/index.html`。

### 内容维护

编辑 `docs/index.html` 中对应的语义化区块：`skills`、`experience`、`projects`、`education`。邮箱与电话链接分别使用 `mailto:` 和 `tel:`；更新显示文字时也应同步更新链接。工作年限及“至今”沿用原简历，后续需手动维护。

所有资源使用相对路径，以兼容根路径与项目子路径部署。站点没有业务 API、请求参数、服务端返回字段或数据提交功能。导航使用页内锚点，简历正文在关闭 JavaScript 时也完整可读。

需要 PDF 时，使用浏览器打印功能（macOS：`⌘P`；Windows：`Ctrl+P`），选择 A4、保存为 PDF，并关闭浏览器附加页眉页脚。打印样式会隐藏导航，保留正文和联系方式。

### GitHub Pages

仓库：`huhaobeiqwq/huhaobeiqwq.github.io`。免费账号使用时仓库应为 Public。

先将页面提交并推送到 `main`，然后进入仓库 `Settings → Pages`：

- Source：`Deploy from a branch`
- Branch：`main`
- Folder：`/docs`

保存后查看部署结果。预期网址为 <https://huhaobeiqwq.github.io/>；仅创建本地文件不会自动发布。

### Cloudflare Pages

在 Cloudflare 控制台进入 `Workers & Pages → Create application → Pages`，选择连接 Git 仓库，授权并选择上述仓库：

| 配置 | 值 |
| --- | --- |
| Production branch | `main` |
| Framework preset | `None` |
| Build command | 留空 |
| Build output directory | `docs` |
| Root directory | 留空，使用仓库根目录 |

执行 `Save and Deploy`，部署后的 `*.pages.dev` 地址以控制台为准。两个平台配置完成后，推送到 `main` 会分别触发自动部署。

官方说明：[GitHub Pages 发布源](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)、[Cloudflare Pages Git 集成](https://developers.cloudflare.com/pages/get-started/git-integration/)。

## 表结构

无数据库，无建表语句。

## checkList

- 核对姓名、联系方式、任职日期、项目职责与奖项内容。
- 检查电脑和手机布局、键盘焦点、站内导航与联系方式链接。
- 检查首页及 CSS 返回成功，根路径和子路径下资源均可加载。
- 检查 A4 打印输出中的分页、正文和联系方式。
- 发布后分别检查两个平台的网址和最新部署状态。
- 本项目不包含自动化测试文件，也不需要编译或安装依赖。