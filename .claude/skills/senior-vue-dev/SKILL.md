---
name: vue-composition-helper
description: 自动优化 Vue 组合式 API代码，提取逻辑为 Composables。
---
当检测到组件内逻辑超过 100 行时，自动激活。
1. 识别独立的业务逻辑块。
2. 将其提取为 `useXxx.ts` 组合式函数。
