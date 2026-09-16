# Ding Ma 个人主页（Jekyll + GitHub Pages）

## 这是什么
- 仓库：https://github.com/dingma-econ/dingma-econ.github.io ；线上：https://dingma-econ.github.io
- Jekyll 站点，Bootstrap 3（LESS 源码）。推送到 `master` 后 GitHub Actions 自动：编译 LESS → `jekyll build` → 推到 `gh-pages` 分支，1–3 分钟生效（Actions 页面可看进度）。
- 三个页面：`pages/_homepage/index.md`（Home）、`pages/_CV/index.md`（CV，只放 PDF 按钮和内嵌预览）、`pages/_research/index.md`（Research）。导航文字在 `_data/categories.yaml`，模板在 `_includes/`。
- CSS/JS/PDF 链接的缓存后缀按构建时间自动生成（`site.time`），不用手动改版本号。

## 常规改动怎么做
- **改内容**：直接改 `pages/` 下的 markdown（里面混着 HTML）。Research 页每篇论文下的 presentations 列表用 `<!-- Presentations ... -->` 注释保留着，需要显示时去掉注释标记即可。
- **主题标签**：`<span class="label label-a">Climate change</span>`。a=蓝 Climate change，b=橙 Health，c=绿 Environment，d=紫 Firm，e=红、f=灰 备用。颜色定义在 `assets/css/_content.less`。
- **样式**：只改 `assets/css/*.less`，绝不直接改 `main.css`（CI 每次重新生成并覆盖）。本机没有 node/ruby，无法本地编译 LESS 或运行 Jekyll，改 LESS 时保持保守，推送后到 Actions 页确认绿色。
- **更新 CV**：把新 PDF 覆盖到 `assets/CV_Ding_Ma_ENG.pdf`，提交推送即可。LaTeX 源码 `CV_for_git_v2.tex` 由本人在 Overleaf 维护；本机装有 MiKTeX（XeLaTeX）和 Georgia 字体，可本地编译：`xelatex --enable-installer -interaction=nonstopmode -halt-on-error cv.tex`（跑两遍）。

## 提交与推送
- 提交者身份已在仓库本地配置（Ding Ma / dingma@njau.edu.cn）；`git push origin master` 直接可用（凭据已通过 Git Credential Manager 保存；若提示 could not read Username，让本人在 VS Code 终端跑一次 `git push` 重新登录）。
- 仓库文件的换行符**逐文件混合**：`_config.yml`、`_includes/footer.html`、`assets/css/_content.less`、`assets/css/_site.less` 是 CRLF，其余是 LF。仓库本地 `core.autocrlf=false`。提交前对比 `git diff --stat` 和 `git diff --ignore-cr-at-eol --stat`，数字不一致说明换行符被改了：用 `tr -d '\r'` 去掉 CR，用 `sed -e 's/$/\r/'` 加 CR。不要信任 `grep -c $'\r'` 或 `sed 's/\r$//'`，在这台机器的 Git Bash 上不可靠。
- 这个环境里 `rm` / `mv -f` 会被权限拒绝；删除文件用 `git rm`，或请本人手动删。超过约 10 KB 的 heredoc 也会失败，大文件用 Write 工具写到 scratchpad 再 `cp`。

## 预览与验证（没有 Jekyll 也能做）
- 拿部署后的 HTML：`git fetch origin gh-pages && git archive origin/gh-pages | tar -x -C <临时目录>`，把 HTML 里的 `"/assets/` 改成相对路径、在 `</head>` 前注入一个 preview.css，就能本地渲染改后效果。
- 截图：`"C:/Program Files (x86)/Microsoft/Edge/Application/msedge.exe" --headless=new --disable-gpu --hide-scrollbars --window-size=1280,1500 --screenshot=out.png <url>`。无头 Edge 有约 500px 的最小窗口，手机宽度要用一个包含 `<iframe width="400">` 的包装页来截。
- 等部署：后台循环 `git ls-remote origin refs/heads/gh-pages` 直到 hash 变化，再等 60–90 秒让 CDN 刷新后再截图。
- 用 Read 工具预览 PDF 时中文可能显示为空白，那是预览渲染的问题，不是 PDF 有问题——先让本人在真实阅读器里确认。

## 本人的偏好
- 首页用第一人称（"I am ..."）；网页上不放办公地址，只写学院和邮箱。
- CV PDF 不压缩页数，节与节之间留足间距；生日保留，手机号已删。
- 三个页面顶部都不放大标题（`no_heading: true`），直接从内容开始。
- 网站不做的事：不要把 presentations 直接删掉（注释保留）；"The Lethal Gains from Trade" 暂不放到网站（CV 里有）。

## 注意
- `_includes/news.html`、`prevnext.html`、`subnav.html`、`toc.html`、`assets/js/search.js` 是模板遗留、未使用，无害，不必动。
- 仓库放在 Dropbox 里时，不要在两台电脑上同时对它执行 git 操作。真正的备份是 GitHub 本身：文件夹丢了可以随时 `git clone` 回来。
