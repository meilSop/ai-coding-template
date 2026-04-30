---
name: db-schema-validator
description: 自动检查数据库设计的规范性。
---
当编写 `.sql` 或 `schema.prisma` 时，自动激活。
1. 检查是否所有表都有主键。
2. 检查是否使用了适当的外键约束。
