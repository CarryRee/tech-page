
## 克隆项目
git clone --recursive https://github.com/CarryRee/tech-page.git

## 发布项目
hugo new posts/hello.md

## 本地预览与正式发布

生产地址已固定在 `hugo.toml`，不需要在每次发布前修改：

```bash
# 本地开发：使用 http://localhost:1313/，并显示 draft 草稿
hugo server

# 正式构建：使用 hugo.toml 中的线上 baseURL，并隐藏 draft 草稿
hugo --minify
```

本地专用设置位于 `config/development/hugo.toml`。文章确认发布时，将文章头部的
`draft = true` 改为 `draft = false`（或删掉该行）后推送到 `main` 即可。
