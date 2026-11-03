# UCAS CCIP Lab 网站

中国科学院大学云计算与智能信息处理实验室（Cloud Computing & Intelligent Information Processing Laboratory，CCIP Lab）网站的**静态发布仓库**，用于保存并发布已经生成的 HTML、CSS、JavaScript、图片和索引文件。

## 访问地址与发布范围

| 入口 | 地址 | 与本仓库的关系 |
| --- | --- | --- |
| GitHub Pages 首页 | <https://tianyuzong.github.io/ucas-ccip-website-pages/> | 本仓库当前的发布站点 |
| GitHub Pages 团队页 | <https://tianyuzong.github.io/ucas-ccip-website-pages/people/> | 查看成员、照片及个人主页 |
| 学校官网 | <https://ccip.ucas.ac.cn/> | 需要通过学校站点的部署流程单独更新 |

**提交到本仓库并完成 GitHub Pages 部署，不代表学校官网已经更新。** 截至 2026 年 11 月 3 日，本仓库的 Pages 设置使用默认 GitHub 域名，没有绑定自定义域名；仓库中未提供学校官网的部署配置或同步脚本。验收发布结果时，应明确检查的是哪个网址。

当前 GitHub Pages 配置：

- 发布方式：`Deploy from a branch`。
- 发布分支与目录：`main` 分支的 `/ (root)`。
- 站点路径前缀：`/ucas-ccip-website-pages/`。
- 部署记录：[Actions](https://github.com/tianyuzong/ucas-ccip-website-pages/actions) 中的 `pages build and deployment`。

## 当前实现

页面中的生成器标记为 **Hugo Blox Builder 5.9.7**。仓库包含浏览器可以直接访问的静态文件，站内搜索由 Fuse.js 读取 `index.json` 完成，数学公式由 MathJax 渲染。

提交历史中的 [bfc35f6](https://github.com/tianyuzong/ucas-ccip-website-pages/commit/bfc35f698d25c119062e19d4271c48a922257dc3) 标注了 `Generated from private source`。本仓库没有完整的 Hugo 内容、模板与构建配置，也没有 `package.json` 或项目测试脚本，因此这里不提供 `npm build` 或 `hugo server` 的源码开发流程。需要修改模板、布局或重新生成网站时，应在对应的源项目中完成。

根目录的 `.nojekyll` 用于让 GitHub Pages 直接发布现有静态文件。

## 目录结构

| 路径 | 内容 |
| --- | --- |
| `index.html` | 网站首页 |
| `people/index.html` | 团队成员列表、分组和头像 |
| `author/<姓名>/` | 成员个人页、订阅文件及部分头像资源 |
| `authors/` | 作者索引页 |
| `research/` | 研究方向 |
| `publication/` | 论文、著作等成果详情与列表 |
| `publication-type/`、`publication_types/` | 成果类型相关页面 |
| `post/` | 新闻动态 |
| `system/`、`teaching/`、`recruit/`、`contact/` | 系统、教学、招生、联系页面 |
| `categories/`、`tags/` | 分类与标签索引 |
| `css/`、`js/`、`zh/js/`、`webfonts/` | 样式、脚本和字体资源 |
| `media/`、`uploads/` | 图片和附件 |
| `index.json` | 站内搜索数据 |
| `index.xml`、各目录的 `index.xml` | RSS 订阅输出 |
| `sitemap.xml`、`robots.txt` | 站点地图与爬虫入口 |
| `404.html`、`manifest.webmanifest` | 错误页与站点清单 |
| `admin/` | 随产物保留的 CMS 页面和配置 |
| `_headers`、`_redirects` | Netlify 格式的配置文件，不是学校服务器部署配置 |

`admin/config.yml` 使用 `git-gateway`，并引用 `content/authors`、`content/publication`、`assets/media` 等源码目录，这些目录不在当前发布仓库中。`admin/` 的存在不代表已经配置好可用的编辑后台。

## 本地预览

预览已有产物只需要 Python 3，无需安装 Hugo 或 Node.js。由于页面资源使用 `/ucas-ccip-website-pages/` 前缀，应从**仓库文件夹的父目录**启动服务，并保留下面的文件夹名称：

```sh
git clone https://github.com/tianyuzong/ucas-ccip-website-pages.git ucas-ccip-website-pages
python3 -m http.server 8000 --bind 127.0.0.1
```

浏览器访问：

- 首页：<http://127.0.0.1:8000/ucas-ccip-website-pages/>
- 团队页：<http://127.0.0.1:8000/ucas-ccip-website-pages/people/>

以上两条命令之间不需要 `cd` 进入仓库。如果已经克隆，请在包含 `ucas-ccip-website-pages` 文件夹的父目录运行第二条命令。使用其他本地目录名时，需要提供同名路径映射，否则根路径引用的样式、脚本和图片可能无法加载。按 `Ctrl+C` 停止预览服务。

本地预览用于检查静态页面；部分外部脚本仍需联网，页面内的绝对链接也可能指向线上站点。

## 内容维护

### 优先在源项目中修改

长期维护应在源项目修改内容并重新生成，再将产物发布到本仓库。直接修改本仓库中的 HTML 可以修正当前页面，但下次从源项目生成时可能被覆盖。需要把这些修正同步回源项目，并在发布流程中保留本 README。

### 成员与教育经历

成员信息主要涉及 `people/index.html` 和 `author/<姓名>/index.html`。维护时同时核对团队列表中的姓名、分组、入学年份，以及个人页中的教育经历。

- 每段教育经历应有明确的入学年份。
- 在读成员当前的教育经历显示为 `入学年份–至今`，例如 `2026–至今`。
- 已完成的教育经历保留实际起止年份，例如 `2022–2026`。
- 预计毕业年份不作为在读经历的结束时间；毕业后再按实际信息更新。
- 修改当前经历时，应保留此前已完成的本科、硕士或博士经历。

当前已补充唐坤、王浩祥、芮雨慧、钟执法、刘浩、王子宁的教育年份，并将当前在读经历统一为“至今”。后续新增成员应采用相同展示规则。

### 成员照片

更换照片时，需要检查团队页头像、个人页头像，以及个人页的 `og:image`、`twitter:image` 和 RSS 中相关图片地址。它们可能引用不同尺寸的旧图片，仅替换某一个文件不一定能覆盖所有位置。

当前陈东杰的照片资源为 `uploads/chendongjie-2026.svg`：该文件在 SVG 中内嵌提供的 JPEG 原图，团队页和个人页通过 CSS 控制裁切。对应引用位于：

- `people/index.html`
- `author/陈东杰/index.html`
- `author/陈东杰/index.xml`

更换文件名后，应同步更新引用，并分别查看团队列表和个人页的显示效果。网页内图片可正常显示不代表各社交平台均支持同样的分享图片格式，分享预览需单独验证。

### 搜索、订阅与链接

这些文件都是已经生成的产物。手工修改 HTML 不会自动更新 `index.json`、RSS 或站点地图；涉及标题、摘要、正文、成员或页面地址变更时，应检查相关索引和链接，优先通过源项目重新生成以保持一致。

## 发布与验收

1. 预览改动，确认页面内容、图片裁切及链接正确。
2. 将改动提交到 `main`（也可以先通过 Pull Request 审核后合并）。
3. 在 [Actions](https://github.com/tianyuzong/ucas-ccip-website-pages/actions) 确认对应提交的 Pages 部署成功。
4. 打开 GitHub Pages 上实际受影响的页面，确认展示的是本次内容。更新成员时至少核对团队页和个人页；必要时刷新以排除浏览器缓存。
5. 如果发布目标还包括学校官网，继续通过学校服务器或其部署项目发布，并在 `https://ccip.ucas.ac.cn/` 单独验收。

学校官网位于域名根路径，而本仓库产物使用 `/ucas-ccip-website-pages/` 前缀。面向学校官网部署时，需要在源项目中配置正确的站点地址并重新生成，或由实际部署流程处理资源路径、canonical 地址和站点地图；不要直接假定复制这份产物到学校站点根目录即可正常工作。

## 反馈

发现页面错误时，可在 [Issues](https://github.com/tianyuzong/ucas-ccip-website-pages/issues) 中附上具体网址、当前内容和期望内容。涉及学校官网时，请明确注明学校域名，便于区分需要更新的发布目标。
