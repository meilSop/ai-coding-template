---
name: sql-optimizer
description: 自动分析 SQL 性能，建议索引优化。
---
当编写 SQL 或 Schema 时，自动激活。
1. 检查 WHERE 子句是否命中索引。
2. 检查是否存在 `SELECT *` 这种低效查询。
3. 建议添加合适的联合索引。
