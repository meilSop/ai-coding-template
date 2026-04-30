---
name: senior-frontend-dev
description: 资深前端开发工程师技能。自动检查前端代码质量、组件规范和性能优化。
triggers:
  - file_pattern: "*.{html,css,scss,js,jsx,ts,tsx,vue}"
---

# 资深前端开发工程师技能

当编写前端代码文件时自动激活。

## 检查清单

### HTML/CSS 检查
- [ ] 语义化 HTML 标签使用正确
- [ ] CSS 选择器优先级合理
- [ ] 响应式设计考虑移动端
- [ ] 可访问性（ARIA 标签）

### JavaScript/TypeScript 检查
- [ ] 类型定义完整（TypeScript）
- [ ] 避免 any 类型滥用
- [ ] 错误处理完善（try-catch）
- [ ] 异步代码使用 async/await
- [ ] 避免内存泄漏（清理定时器、事件监听）

### React 组件检查
- [ ] 使用函数组件和 Hooks
- [ ] Props 类型定义完整
- [ ] useEffect 依赖数组完整
- [ ] 性能优化（useMemo, useCallback）
- [ ] 组件拆分合理（单一职责）

### Vue 组件检查
- [ ] 使用 Composition API
- [ ] Props/Emits 类型定义完整
- [ ] 响应式数据使用 ref/reactive 正确
- [ ] 生命周期钩子使用恰当

### 性能优化检查
- [ ] 图片懒加载和压缩
- [ ] 代码分割（Code Splitting）
- [ ] 资源缓存策略
- [ ] 避免不必要的重渲染
- [ ] 关键渲染路径优化

### 代码规范检查
- [ ] ESLint 规则通过
- [ ] Prettier 格式化
- [ ] 命名规范一致（驼峰、帕斯卡）
- [ ] 注释清晰有意义
- [ ] 无 console.log 遗留（生产代码）

## 自动修复建议

当发现问题时，提供以下类型的修复：

1. **类型修复**：补充 TypeScript 类型定义
2. **性能修复**：添加 useMemo/useCallback 优化
3. **规范修复**：调整代码格式和命名
4. **安全修复**：处理 XSS、CSRF 等安全风险

## 最佳实践提示

- 优先使用现代前端特性（ES2020+）
- 遵循框架官方最佳实践
- 保持组件小而聚焦
- 关注用户体验和可访问性
- 编写可测试的代码
