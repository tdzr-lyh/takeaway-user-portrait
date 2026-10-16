# 只使用 GitHub 的用户画像网站

这个版本只使用 GitHub 仓库、GitHub Actions 和 GitHub Pages，不依赖 Render 或自己的服务器。
在免费账号的公开仓库中发布，使用 GitHub 提供的 HTTPS 地址，不购买域名。

## 功能

保留数据总览、单用户画像、五类群体画像、流失风险筛选/升降序/分页、模型实验结果和方法说明。
98,673 名样本用户均可查询。首页和群体图表由本地 ECharts 绘制。
单用户数据每 1,000 人一片，风险名单每 400 人一片，访问时按需读取，不一次下载全部数据。
算法仍使用原 Python 项目的真实实验结果，GitHub 上不运行 Flask、SQLite 或模型训练。
如果需要更新数据，重新导出并上传 site.zip；这不是实时写入数据库的后台服务。

## 发布步骤

1. 创建公开仓库，例如 `takeaway-user-portrait`。为了使用免费 Pages，个人免费账号请选 Public。
2. 把本包中的 `site.zip` 和 `README.md` 上传仓库根目录。不要解压后逐个上传上千个数据文件。
3. 新建文件 `.github/workflows/pages.yml`，复制本包相同路径文件的内容并提交。
4. 打开仓库 Settings → Pages，Build and deployment 的 Source 选择 GitHub Actions。
5. 打开 Actions → Publish GitHub Pages，若之前因 Pages 未启用而失败，选择 Re-run jobs，
   或通过 Run workflow 手动运行。首次也可能需要在 Actions 页面启用工作流。
6. 等待绿色成功状态，打开部署步骤或 Settings → Pages 中显示的真实网站地址。

常见地址形式为 `https://你的用户名.github.io/仓库名/`，实际地址以 GitHub 显示为准。
页面均使用相对路径，兼容仓库子目录。关闭本机后用手机移动网络复测。
此包本身没有发布到你的账号，只有工作流成功后才有可访问的公网网站。

## 数据可见性

这是公开静态演示网站，访客可以下载导出的 JSON；去除了姓名、原始 CSV 和未展示字段，
仍保留样本编号、年龄、省份、注册渠道和行为指标。请仅用作当前论文样本演示。
包内没有论文、原始数据库、密码、虚拟环境或访问密钥。

## 费用与限制

公开仓库内的 Pages 和标准 GitHub 托管 Actions 可免费使用，发布时不启用付费功能。
GitHub Pages 有站点大小、流量及使用场景限制，当前网站适合论文演示，不能保证所有地区网络都畅通。
本项目没有添加防休眠请求或外部托管，也没有购买服务器。
请通过发布的网址访问；直接双击电脑里的 HTML 时，浏览器可能阻止 JSON 请求。

## 代码位置

原 Flask 项目保留。静态前端源码位于 `first/deploy/pages/`，导出脚本为
`first/deploy/package_pages.py`，无需把本机 Python 环境上传 GitHub。

官方说明：
- https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages
- https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits
- https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages
