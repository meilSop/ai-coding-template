---
name: micro-frontend-isolation
description: 自动检查微前端的隔离策略。
---
当修改微前端配置文件时，自动激活。
1. 检查 CSS 是否使用了唯一的前缀或 Shadow DOM。
2. 检查 `publicPath` 配置是否为动态运行时注入。
