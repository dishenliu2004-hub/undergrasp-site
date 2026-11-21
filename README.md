# UnderGrasp 论文项目网站

这是可编辑的 Astro 单页静态网站源码。页面使用的论文 PDF、视频、封面和实验图都随包提供。

## 本地预览

准备 Node.js 22 或 24 及 npm。解压后，在包含 `package.json` 的目录打开终端，依次运行：

```sh
source ~/.nvm/nvm.sh
nvm use 22
npm run dev
```

用浏览器打开终端显示的本地地址。编辑源码后，预览会自动刷新。第一次安装依赖需要访问 npm 公共仓库。

## 修改入口

| 位置 | 用途 |
| --- | --- |
| `src/pages/index.astro` | 页面正文、作者、论文和仓库链接及 BibTeX。文件开头的 `trials` 和 `results` 分别定义实验选项与成绩表。 |
| `src/styles/site.css` | 排版、视频尺寸、切换按钮、移动端布局。 |
| `public/media/` | 论文、视频和图片。保留文件名即可直接替换素材。 |
| `package-lock.json` | 记录构建依赖的确切版本，随源码一并保留。 |

四个实验视频的文件名依次为 `single.mp4`、`clutter.mp4`、`comparison.mp4`、`transport.mp4`，各自搭配同名 JPG 封面。第四项还会切换实验说明，并在右侧显示 `transport-results.png`。论文文件为 `undergrasp.pdf`。

首页的 **Code** 按钮通过 `src/pages/index.astro` 开头的 `githubUrl` 跳转到 UnderGrasp 代码仓库。**arXiv** 按钮在 `arxivUrl` 为空时显示为不可点击的占位。论文上线后，将 arXiv 摘要页的 HTTPS 地址填入 `arxivUrl`。

## 构建并放到网站

部署在独立域名首页时运行：

```sh
npm run build
npm run preview
```

预览确认后，将生成的 `dist/` **里面的全部内容**上传到网站根目录，包含 `index.html`、`_astro/` 和 `media/`。线上只需提供静态文件服务。

如果页面是现有网站下的子目录，例如 `https://example.org/projects/undergrasp/`，使用实际 URL 路径构建：

```sh
npm run build -- --base /projects/undergrasp
```

将这次生成的 `dist/` 内容放入网站的 `projects/undergrasp/` 目录，通过带末尾斜杠的项目网址访问。若使用自动构建平台，安装命令填 `npm ci`，构建命令按上述目标路径填写，输出目录填 `dist`。

## 发布到 GitHub Pages

首次推送 `main` 后，在 GitHub 仓库的 **Settings → Pages → Build and deployment → Source** 中选择 **GitHub Actions**，再到 **Actions** 手动运行 **Deploy UnderGrasp to GitHub Pages**。部署成功后，从 **Settings → Pages** 打开网页。后续推送到 `main` 时会自动部署，工作流会读取实际站点的路径来构建页面。
