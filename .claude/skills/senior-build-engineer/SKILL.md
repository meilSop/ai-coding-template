---
name: bundle-analyzer
description: 自动分析构建产物并优化配置。
---
当修改构建配置文件时，自动激活。
1. 检查是否开启了 SourceMap（生产环境应关闭）。
2. 检查是否配置了 `alias` 以减少路径解析开销。
