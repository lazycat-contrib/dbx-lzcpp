# DBX for LazyCat

DBX 的 LazyCat LPK v2 打包项目。上游项目：<https://github.com/t8y2/dbx>。

DBX 是一款约 20 MB 的轻量级跨平台数据库管理工具，支持 MySQL、PostgreSQL、SQLite、Redis、MongoDB、DuckDB、SQL Server、达梦等 90+ 数据库，并提供 AI 助手、MCP Server、CLI、桌面端和 Docker 版本。

## 部署设置

安装向导会配置以下环境变量：

- `DBX_PASSWORD`：DBX Web 登录密码，默认生成随机密码，并通过 LazyCat 浏览器注入自动填充。
- `DBX_WEB_MCP_TOKEN`：Web MCP 认证令牌，默认生成随机长密钥。
- `DBX_WEB_MCP_ALLOWED_HOSTS`：Web MCP 允许的 Host，默认 `localhost:4224`。
- `DBX_WEB_MCP_ALLOWED_ORIGINS`：浏览器 MCP 客户端允许的 Origin，默认 `*`。

应用数据持久化到 `/lzcapp/var/dbx`。文件导入和导出已接入 LazyCat 文件选择器拦截。

## 自动发布

GitHub Actions 每日检查 `t8y2/dbx` 的稳定 SemVer 镜像标签，使用 Docker Hub 默认镜像加速地址并校验目标镜像摘要。工作流仅发布到喵喵私有商店，不发布到官方商店。

需要让以下 GitHub Secrets 对本仓库可用：

- `APPSTORE_URL`
- `APPSTORE_TOKEN`
- `APP_ID`（可选）
- `PRIVATE_STORE_GROUP_CODES`（可选）

构建产物使用版本化 Release Asset：`community.lazycat.app.dbx-v<version>.lpk`。

## 本地构建

```bash
lzc-cli project release -o dist/dbx.lpk
lzc-cli lpk info dist/dbx.lpk
```
