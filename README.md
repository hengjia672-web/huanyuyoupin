# 寰宇优品 / 达人选品系统 — 数据库异地备份

每周自动从腾讯云轻量服务器 MySQL 导出 SQL，转储为 .sql.gz 后提交到此仓库。

## 备份机制

- 服务器：腾讯云轻量 (OpenCloudOS 9.6)
- 数据库：MySQL 8（Docker 容器 daren_selection_db）
- 工具：mysqldump + gzip + git push
- 调度：cron 每周一 03:00
- 保留：最近 8 周（约 2 个月）
- 凭据：SSH key（专用，不复用任何业务密钥）

## 文件命名

`daren_<YYYYMMDD_HHMMSS>.sql.gz`

每个文件是一个独立完整快照（不增量），可直接 `gunzip` + `mysql < ...` 还原。
