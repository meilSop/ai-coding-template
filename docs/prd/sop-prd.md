# SOP (Scaffold Operating Platform) 前端框架 PRD

## 1. 背景与目标

### 1.1 背景

目前 Vue3 生态已趋于成熟，但在后台管理系统开发场景中，开发者仍需重复搭建项目基础设施（路由、权限、状态管理、布局等），且 Element Plus 等基础组件库偏原子化，需要大量模板代码才能完成业务功能。

### 1.2 目标

打造一款**开箱即用的 Vue3 后台管理二次开发框架 SOP (Scaffold Operating Platform)**，通过配置化组件、Hooks 封装、多套主题方案，帮助开发者快速搭建企业级后台系统。

### 1.3 目标用户

- 中高级前端开发者
- 需要快速交付后台管理系统的技术团队
- 寻求 Vue3 最佳实践参考的学习者

---

## 2. 功能清单（MoSCoW 优先级）

### Must Have（必须有）

| 模块     | 功能       | 描述                                                          |
| -------- | ---------- | ------------------------------------------------------------- |
| 基础设施 | 项目脚手架 | CLI 工具快速创建项目模板                                      |
|          | 工程化配置 | TypeScript + ESLint + Prettier + Husky                        |
|          | 路由系统   | Vue Router 4 + 动态路由 + 路由守卫                            |
|          | 状态管理   | Pinia + 持久化插件（pinia-plugin-persistedstate）             |
|          | HTTP 封装  | Axios 封装 + 拦截器（统一错误处理、请求/响应转换）            |
|          | 国际化     | Vue I18n + 语言切换 + 语言包管理                              |
| 布局系统 | 上下布局   | 顶部导航栏 + 内容区                                           |
|          | 左右布局   | 侧边栏菜单 + 内容区                                           |
|          | 混合布局   | 顶部导航 + 侧边栏 + 内容区                                    |
|          | 菜单管理   | 多级菜单、菜单折叠、菜单搜索                                  |
| 权限认证 | 登录页面   | 账号密码登录、记住密码                                        |
|          | 注册页面   | 用户注册                                                      |
|          | JWT 管理   | Token 获取、自动刷新、登出清除                                |
|          | 路由权限   | 基于角色的路由守卫                                            |
| 组件封装 | Form 表单  | JSON Schema 驱动配置化表单 sop-form（基于 Element Plus）      |
|          | Table 表格 | 基于 Vxe-Table 封装的配置化表格 sop-table（分页、排序、筛选） |

### Should Have（应该有）

| 模块     | 功能         | 描述                                                     |
| -------- | ------------ | -------------------------------------------------------- |
| 组件封装 | Upload 上传  | 图片/文件上传 sop-upload、分片上传、图片压缩             |
|          | Echarts 图表 | 常用图表封装 sop-echarts（柱状图、折线图、饼图、仪表盘） |
|          | SearchForm   | 搜索表单组件 sop-search（展开/收起）                     |
| 权限认证 | 按钮权限     | `v-permission` 指令控制按钮显示                          |
|          | 多种登录     | 手机号登录、扫码登录                                     |
| 主题系统 | 多套主题     | 浅色主题、深色主题、高对比主题                           |
|          | 主题定制     | 在线主题工具（可视化修改变量）                           |
| 示例项目 | 后台模板     | 完整的后台管理系统示例                                   |
|          | 组件示例     | 各组件的使用示例页面                                     |

### Could Have（可以有）

| 模块     | 功能         | 描述                        |
| -------- | ------------ | --------------------------- |
| 组件封装 | 富文本编辑器 | 基于 Quill/TinyMCE 封装     |
|          | 代码编辑器   | 基于 Monaco 封装            |
|          | 树形表格     | 支持展开/折叠的树形数据表格 |
| 示例项目 | 数据大屏     | 数据可视化大屏模板          |
|          | 表单构建器   | 拖拽式表单设计器            |

### Won't Have（暂不做）

| 功能           | 原因                                      |
| -------------- | ----------------------------------------- |
| SSR 服务端渲染 | 定位为纯前端框架，后台系统对 SEO 要求不高 |
| 跨平台支持     | 专注 PC 端后台管理，暂不支持小程序/桌面端 |
| 低代码/无代码  | 目标用户为中高级开发者，配置化已满足需求  |

---

## 3. 架构设计

### 3.1 SOP 主仓库结构

```
sop/                                      # SOP 主仓库
├── packages/                               # 包目录
│   ├── lib/                                # 核心库 (@sop/lib)
│   │   ├── package.json
│   │   ├── src/
│   │   │   ├── core/                       # 核心功能
│   │   │   │   ├── router/                 # 路由管理
│   │   │   │   ├── store/                  # 状态管理
│   │   │   │   ├── request/                # HTTP 请求
│   │   │   │   ├── auth/                   # 权限认证
│   │   │   │   ├── i18n/                   # 国际化
│   │   │   │   ├── layout/                 # 布局系统
│   │   │   │   ├── theme/                  # 主题系统
│   │   │   │   ├── hooks/                  # 通用 Hooks
│   │   │   │   └── utils/                  # 工具函数
│   │   │   └── components/                 # 业务组件
│   │   │       ├── sop-form/               # 表单组件（基于 Element Plus）
│   │   │       ├── sop-table/              # 表格组件（基于 Vxe-Table）
│   │   │       ├── sop-upload/
│   │   │       ├── sop-echarts/
│   │   │       ├── sop-search/
│   │   │       └── common/
│   │   └── index.ts
│   │
│   ├── pages/                              # 业务页面库 (@sop/pages)
│   │   ├── package.json
│   │   ├── src/
│   │   │   ├── views/                      # 通用业务页面
│   │   │   │   ├── login/
│   │   │   │   ├── register/
│   │   │   │   ├── dashboard/
│   │   │   │   ├── system/
│   │   │   │   │   ├── user/
│   │   │   │   │   ├── role/
│   │   │   │   │   └── menu/
│   │   │   │   └── ...
│   │   │   ├── router/
│   │   │   └── api/
│   │   └── index.ts
│   │
│   └── cli/                                # CLI 工具 (@sop/cli)
│       ├── package.json
│       ├── bin/
│       │   └── sop.js
│       ├── src/
│       │   ├── create.ts
│       │   ├── template/
│       │   └── utils/
│       └── README.md
│
├── package.json
├── pnpm-workspace.yaml
├── tsconfig.json
├── README.md
└── CHANGELOG.md
```

### 3.2 pc-template 模板工程

```
pc-template/                                # PC 端模板工程（独立仓库）
│
├── packages/                               # 依赖包（git submodule）
│   ├── lib/                                # 指向 sop/packages/lib
│   │   └── src/                            # git submodule
│   │       ├── core/
│   │       ├── components/
│   │       └── ...
│   │
│   └── pages/                              # 指向 sop/packages/pages
│       └── src/                            # git submodule
│           ├── views/
│           ├── router/
│           └── ...
│
├── play/                                   # 业务开发目录
│   ├── src/
│   │   ├── views/                          # 业务页面
│   │   │   ├── business/
│   │   │   ├── project/
│   │   │   └── ...
│   │   ├── router/                         # 业务路由
│   │   │   ├── index.ts
│   │   │   └── routes.ts
│   │   ├── api/                            # 业务接口
│   │   │   ├── business.ts
│   │   │   └── ...
│   │   ├── stores/                         # 业务状态
│   │   ├── components/                       # 业务组件
│   │   └── main.ts
│   ├── package.json
│   ├── tsconfig.json
│   └── vite.config.ts
│
├── package.json                            # workspace 根配置
├── pnpm-workspace.yaml                     # pnpm workspace 配置
├── .gitmodules                               # git submodule 配置
├── .npmrc                                    # npm 配置
├── .gitignore
├── README.md
└── CHANGELOG.md
```

### 3.3 Git Submodule 配置

```ini
# .gitmodules
[submodule "packages/lib"]
    path = packages/lib
    url = https://github.com/your-org/sop.git
    branch = main

[submodule "packages/pages"]
    path = packages/pages
    url = https://github.com/your-org/sop.git
    branch = main
```

### 3.4 pnpm Workspace 配置

```yaml
# pnpm-workspace.yaml
packages:
  - 'packages/*'
  - 'play'
```

```json
// package.json (pc-template)
{
  "name": "pc-template",
  "private": true,
  "workspaces": ["packages/*", "play"],
  "scripts": {
    "dev": "pnpm -F play dev",
    "build": "pnpm -F play build",
    "preview": "pnpm -F play preview",
    "update:submodules": "git submodule update --remote",
    "commit:submodules": "git add packages/lib packages/pages && git commit -m \"chore: update submodules\""
  }
}
```

---

## 4. 用户故事与验收标准

### 用户故事 1: 作为开发者，我希望通过 CLI 快速创建项目

**验收标准:**

1. [ ] 提供 CLI 命令 `npm create sop <project-name>` 创建项目
2. [ ] 支持选择模板类型（基础版/完整版/pc-template）
3. [ ] 项目初始化后运行 `npm install && npm run dev` 可直接启动
4. [ ] 生成的项目包含完整的目录结构、路由配置、状态管理
5. [ ] README 包含快速开始、项目结构、开发规范说明

### 用户故事 2: 作为开发者，我希望使用配置化表单快速开发

**验收标准:**

1. [ ] Form 组件支持通过 JSON Schema 配置生成表单
2. [ ] 内置常用表单字段类型（input、select、date、upload 等）
3. [ ] 支持表单验证规则配置（required、pattern、自定义校验）
4. [ ] 支持表单布局配置（inline、horizontal、vertical）
5. [ ] 提供完整的 TypeScript 类型定义
6. [ ] 文档包含 5+ 个常见使用场景示例

### 用户故事 3: 作为开发者，我希望使用配置化表格快速开发

**验收标准:**

1. [ ] Table 组件基于 Vxe-Table 二次封装，支持通过 JSON Schema 配置生成表格列
2. [ ] 内置分页功能，支持前端/后端分页切换
3. [ ] 支持列排序、列筛选配置
4. [ ] 支持行选择（单选/多选）和批量操作
5. [ ] 支持操作列自定义（编辑/删除/查看等按钮）
6. [ ] 支持表格数据导出（Excel/CSV）
7. [ ] 文档包含 5+ 个常见使用场景示例

### 用户故事 4: 作为开发者，我希望使用开箱即用的布局系统

**验收标准:**

1. [ ] 支持三种布局模式：上下布局、左右布局、混合布局
2. [ ] 布局切换通过配置项控制，无需修改业务代码
3. [ ] 侧边栏菜单支持多级嵌套、折叠/展开、菜单搜索
4. [ ] 顶部导航支持面包屑、全屏、Icon Park 图标、语言切换、用户菜单
5. [ ] 布局组件响应式适配，适配主流屏幕尺寸
6. [ ] 提供完整的布局配置文档

### 用户故事 5: 作为开发者，我希望框架提供完整的权限认证方案

**验收标准:**

1. [ ] 提供登录页面模板，支持账号密码登录
2. [ ] 提供注册页面模板
3. [ ] JWT Token 管理：登录获取、自动刷新、登出清除
4. [ ] 路由守卫：未登录自动跳转登录页，无权限跳转 403 页
5. [ ] 菜单权限：根据用户角色动态渲染菜单
6. [ ] 按钮权限：提供 `v-permission` 指令控制按钮显示/隐藏
7. [ ] 提供完整的权限配置文档

---

## 5. 业务规则

### 核心规则

| 规则编号 | 规则描述        | 说明                                                                                                         |
| -------- | --------------- | ------------------------------------------------------------------------------------------------------------ |
| R001     | 组件命名规范    | 所有业务组件以 `sop-` 开头（如 sop-form、sop-table），采用 kebab-case 命名，避免与 Element Plus 组件命名冲突 |
| R002     | 组合式 API 优先 | 所有组件和逻辑封装使用 Vue 3 Composition API                                                                 |
| R003     | Hooks 逻辑复用  | 业务逻辑通过自定义 Hooks 封装（如 useTable、useForm、usePermission）                                         |
| R004     | 配置化优先      | 优先通过 JSON Schema 配置生成 UI，减少模板代码                                                               |
| R005     | 类型安全        | 所有组件和 API 必须提供完整的 TypeScript 类型定义                                                            |
| R006     | 国际化支持      | 所有 UI 文本必须通过 Vue I18n 支持国际化                                                                     |

### 辅助规则

| 规则编号 | 规则描述 | 说明                                                                         |
| -------- | -------- | ---------------------------------------------------------------------------- |
| R102     | 图标规范 | 统一使用 `@icon-park/vue-next` 图标库，支持多主题风格（线性/填充/双色/多色） |
| R103     | 代码规范 | ESLint + Prettier 统一代码风格，提交前自动格式化                             |
| R104     | 提交规范 | Commit message 遵循 Conventional Commits 规范                                |
| R105     | 文件组织 | 组件、Hooks、Utils 按功能模块组织，避免扁平化目录                            |

### 数据规则

| 规则编号 | 规则描述 | 说明                                                                     |
| -------- | -------- | ------------------------------------------------------------------------ |
| R201     | 接口规范 | 统一 RESTful API 响应格式 `{ code: number, data: any, message: string }` |
| R202     | 状态管理 | 全局状态按功能模块划分 Store，避免单文件过大                             |
| R203     | 缓存策略 | 路由组件按需缓存（keep-alive），接口数据按业务需求缓存                   |
| R204     | 本地存储 | 敏感信息使用 sessionStorage，持久化配置使用 localStorage                 |
| R205     | 表单验证 | 表单验证规则统一定义，支持同步和异步验证                                 |

---

## 6. 异常处理

| 异常场景       | 错误码/提示        | 处理方式                                  |
| -------------- | ------------------ | ----------------------------------------- |
| 网络请求超时   | `NET_TIMEOUT`      | 显示"请求超时，请稍后重试"，提供重试按钮  |
| 网络请求失败   | `NET_ERROR`        | 显示"网络连接失败，请检查网络设置"        |
| 接口返回 401   | `UNAUTHORIZED`     | 清除 Token，跳转登录页                    |
| 接口返回 403   | `FORBIDDEN`        | 跳转 403 页面或显示"无权访问"提示         |
| 接口返回 404   | `NOT_FOUND`        | 跳转 404 页面                             |
| 接口返回 500   | `SERVER_ERROR`     | 显示"服务器繁忙，请稍后重试"              |
| 表单验证失败   | `VALIDATION_ERROR` | 高亮错误字段，显示具体错误信息            |
| Token 刷新失败 | `REFRESH_FAILED`   | 清除过期 Token，跳转登录页                |
| 路由不存在     | `ROUTE_NOT_FOUND`  | 跳转 404 页面                             |
| 组件渲染异常   | `RENDER_ERROR`     | 显示 Error Boundary 兜底 UI，记录错误日志 |

---

## 7. 非功能需求

### 性能需求

| 指标               | 目标值  | 说明                          |
| ------------------ | ------- | ----------------------------- |
| 首屏加载时间       | < 3s    | 4G 网络环境下                 |
| 组件懒加载         | 100%    | 路由级 Code Splitting         |
| 打包体积（gzip）   | < 300KB | 核心框架（不含 Element Plus） |
| 运行时内存         | < 100MB | 典型后台管理系统场景          |
| 路由切换           | < 200ms | 从点击到渲染完成              |
| 列表渲染（1000条） | < 1s    | 虚拟滚动场景下                |

### 可维护性需求

| 项目     | 要求                                          |
| -------- | --------------------------------------------- |
| 代码规范 | ESLint + Prettier + Husky 提交前检查          |
| 类型覆盖 | TypeScript 类型定义 100% 覆盖公共 API         |
| 单元测试 | 核心工具函数和 Hooks 覆盖率 > 80%             |
| 组件文档 | VitePress 组件文档                            |
| 变更日志 | 遵循 Conventional Commits，自动生成 CHANGELOG |
| 版本规范 | 遵循 Semver 语义化版本规范                    |

### 兼容性需求

| 项目         | 支持版本 |
| ------------ | -------- |
| Chrome/Edge  | 90+      |
| Firefox      | 88+      |
| Safari       | 14+      |
| Node.js      | 18+      |
| Vue          | 3.3+     |
| Element Plus | 2.4+     |
| Vxe-Table    | 4.5+     |

---

## 8. 里程碑与开发计划

**总工期：4 周（20 个工作日）**

### 里程碑规划

| 阶段   | 里程碑                                     | 预计周期 |
| ------ | ------------------------------------------ | -------- |
| **M1** | 基础设施搭建                               | 2 周     |
|        | - 项目脚手架 + CLI 工具 (@sop/cli)         |          |
|        | - packages/lib 核心库 (core + components)  |          |
|        | - 工程化配置（ESLint/Prettier/TypeScript） |          |
| **M2** | 核心组件开发                               | 3 周     |
|        | - VForm 表单组件（基于 Element Plus）      |          |
|        | - VTable 表格组件（基于 Vxe-Table）        |          |
|        | - Upload 上传组件                          |          |
| **M3** | 权限与高级组件                             | 2 周     |
|        | - Echarts 图表组件                         |          |
|        | - 登录/注册页面模板                        |          |
|        | - JWT 权限认证                             |          |
|        | - 按钮级权限控制                           |          |
| **M4** | 模板、文档与发布                           | 2 周     |
|        | - packages/pages 业务页面库                |          |
|        | - pc-template 模板工程                     |          |
|        | - VitePress 文档站点                       |          |
|        | - 发布到 npm                               |          |

---

## 9. 项目结构

### 9.1 SOP 主仓库

```
sop/                                      # SOP 主仓库
├── packages/
│   ├── lib/                                # 核心库 (@sop/lib)
│   │   ├── package.json
│   │   ├── src/
│   │   │   ├── core/                       # 核心功能
│   │   │   │   ├── router/
│   │   │   │   ├── store/
│   │   │   │   ├── request/
│   │   │   │   ├── auth/
│   │   │   │   ├── i18n/
│   │   │   │   ├── layout/
│   │   │   │   ├── theme/
│   │   │   │   ├── hooks/
│   │   │   │   └── utils/
│   │   │   └── components/               # 业务组件
│   │   │       ├── VForm/                # 基于 Element Plus
│   │   │       ├── VTable/               # 基于 Vxe-Table
│   │   │       ├── sop-upload/
│   │   │       ├── sop-echarts/
│   │   │       ├── sop-search/
│   │   │       └── common/
│   │   └── index.ts
│   │
│   ├── pages/                              # 业务页面库 (@sop/pages)
│   │   ├── package.json
│   │   ├── src/
│   │   │   ├── views/                      # 通用业务页面
│   │   │   │   ├── login/
│   │   │   │   ├── register/
│   │   │   │   ├── dashboard/
│   │   │   │   ├── system/
│   │   │   │   │   ├── user/
│   │   │   │   │   ├── role/
│   │   │   │   │   └── menu/
│   │   │   │   └── ...
│   │   │   ├── router/
│   │   │   └── api/
│   │   └── index.ts
│   │
│   └── cli/                                # CLI 工具 (@sop/cli)
│       ├── package.json
│       ├── bin/
│       │   └── sop.js
│       ├── src/
│       │   ├── create.ts
│       │   ├── template/
│       │   └── utils/
│       └── README.md
│
├── package.json
├── pnpm-workspace.yaml
├── tsconfig.json
├── README.md
└── CHANGELOG.md
```

### 9.2 pc-template 模板工程

```
pc-template/                                # PC 端模板工程（独立仓库）
├── packages/                               # 依赖包（git submodule）
│   ├── lib/                                # 指向 sop/packages/lib
│   │   └── src/
│   └── pages/                              # 指向 sop/packages/pages
│       └── src/
│
├── play/                                   # 业务开发目录
│   ├── src/
│   │   ├── views/                          # 业务页面
│   │   ├── router/                         # 业务路由
│   │   ├── api/                            # 业务接口
│   │   └── main.ts
│   └── package.json
│
├── package.json                            # workspace 根配置
├── pnpm-workspace.yaml                     # pnpm workspace 配置
├── .gitmodules                               # git submodule 配置
└── README.md
```

### 9.3 关键技术配置

#### Git Submodule 配置

```ini
# .gitmodules
[submodule "packages/lib"]
    path = packages/lib
    url = https://github.com/your-org/sop.git
    branch = main

[submodule "packages/pages"]
    path = packages/pages
    url = https://github.com/your-org/sop.git
    branch = main
```

#### pnpm Workspace 配置

```yaml
# pnpm-workspace.yaml
packages:
  - 'packages/*'
  - 'play'
```

```json
{
  "name": "pc-template",
  "private": true,
  "workspaces": ["packages/*", "play"],
  "scripts": {
    "dev": "pnpm -F play dev",
    "build": "pnpm -F play build",
    "update:submodules": "git submodule update --remote"
  }
}
```

---

## 10. 用户故事与验收标准

### 用户故事 1: 作为开发者，我希望通过 CLI 快速创建项目

**验收标准:**

1. [ ] 提供 CLI 命令 `npm create sop <project-name>` 创建项目
2. [ ] 支持选择模板类型（基础版/完整版/pc-template）
3. [ ] 项目初始化后运行 `npm install && npm run dev` 可直接启动
4. [ ] 生成的项目包含完整的目录结构、路由配置、状态管理
5. [ ] README 包含快速开始、项目结构、开发规范说明

### 用户故事 2: 作为开发者，我希望使用配置化表单快速开发

**验收标准:**

1. [ ] Form 组件支持通过 JSON Schema 配置生成表单
2. [ ] 内置常用表单字段类型（input、select、date、upload 等）
3. [ ] 支持表单验证规则配置（required、pattern、自定义校验）
4. [ ] 支持表单布局配置（inline、horizontal、vertical）
5. [ ] 提供完整的 TypeScript 类型定义
6. [ ] 文档包含 5+ 个常见使用场景示例

### 用户故事 3: 作为开发者，我希望使用配置化表格快速开发

**验收标准:**

1. [ ] Table 组件基于 Vxe-Table 二次封装，支持通过 JSON Schema 配置生成表格列
2. [ ] 内置分页功能，支持前端/后端分页切换
3. [ ] 支持列排序、列筛选配置
4. [ ] 支持行选择（单选/多选）和批量操作
5. [ ] 支持操作列自定义（编辑/删除/查看等按钮）
6. [ ] 支持表格数据导出（Excel/CSV）
7. [ ] 文档包含 5+ 个常见使用场景示例

### 用户故事 4: 作为开发者，我希望使用开箱即用的布局系统

**验收标准:**

1. [ ] 支持三种布局模式：上下布局、左右布局、混合布局
2. [ ] 布局切换通过配置项控制，无需修改业务代码
3. [ ] 侧边栏菜单支持多级嵌套、折叠/展开、菜单搜索
4. [ ] 顶部导航支持面包屑、全屏、Icon Park 图标、语言切换、用户菜单
5. [ ] 布局组件响应式适配，适配主流屏幕尺寸
6. [ ] 提供完整的布局配置文档

### 用户故事 5: 作为开发者，我希望框架提供完整的权限认证方案

**验收标准:**

1. [ ] 提供登录页面模板，支持账号密码登录
2. [ ] 提供注册页面模板
3. [ ] JWT Token 管理：登录获取、自动刷新、登出清除
4. [ ] 路由守卫：未登录自动跳转登录页，无权限跳转 403 页
5. [ ] 菜单权限：根据用户角色动态渲染菜单
6. [ ] 按钮权限：提供 `v-permission` 指令控制按钮显示/隐藏
7. [ ] 提供完整的权限配置文档

---

## 11. 业务规则

### 核心规则

| 规则编号 | 规则描述        | 说明                                                                                                         |
| -------- | --------------- | ------------------------------------------------------------------------------------------------------------ |
| R001     | 组件命名规范    | 所有业务组件以 `sop-` 开头（如 sop-form、sop-table），采用 kebab-case 命名，避免与 Element Plus 组件命名冲突 |
| R002     | 组合式 API 优先 | 所有组件和逻辑封装使用 Vue 3 Composition API                                                                 |
| R003     | Hooks 逻辑复用  | 业务逻辑通过自定义 Hooks 封装（如 useTable、useForm、usePermission）                                         |
| R004     | 配置化优先      | 优先通过 JSON Schema 配置生成 UI，减少模板代码                                                               |
| R005     | 类型安全        | 所有组件和 API 必须提供完整的 TypeScript 类型定义                                                            |
| R006     | 国际化支持      | 所有 UI 文本必须通过 Vue I18n 支持国际化                                                                     |

### 辅助规则

| 规则编号 | 规则描述 | 说明                                                                         |
| -------- | -------- | ---------------------------------------------------------------------------- |
| R102     | 图标规范 | 统一使用 `@icon-park/vue-next` 图标库，支持多主题风格（线性/填充/双色/多色） |
| R103     | 代码规范 | ESLint + Prettier 统一代码风格，提交前自动格式化                             |
| R104     | 提交规范 | Commit message 遵循 Conventional Commits 规范                                |
| R105     | 文件组织 | 组件、Hooks、Utils 按功能模块组织，避免扁平化目录                            |

### 数据规则

| 规则编号 | 规则描述 | 说明                                                                     |
| -------- | -------- | ------------------------------------------------------------------------ |
| R201     | 接口规范 | 统一 RESTful API 响应格式 `{ code: number, data: any, message: string }` |
| R202     | 状态管理 | 全局状态按功能模块划分 Store，避免单文件过大                             |
| R203     | 缓存策略 | 路由组件按需缓存（keep-alive），接口数据按业务需求缓存                   |
| R204     | 本地存储 | 敏感信息使用 sessionStorage，持久化配置使用 localStorage                 |
| R205     | 表单验证 | 表单验证规则统一定义，支持同步和异步验证                                 |

---

## 12. 技术栈

- **框架**：Vue 3.3+
- **UI 库**：Element Plus 2.4+
- **表格组件**：Vxe-Table 4.5+
- **构建工具**：Vite 5+
- **类型系统**：TypeScript 5+
- **状态管理**：Pinia
- **路由**：Vue Router 4
- **HTTP**：Axios
- **国际化**：Vue I18n
- **图标库**：@icon-park/vue-next
- **包管理**：pnpm
- **工作区**：pnpm workspace + git submodule

---

## 13. 变更日志

| 版本   | 日期       | 变更内容                                                                                                                                               |
| ------ | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| v1.0.0 | 2024-02-01 | 初始版本发布，框架名称 SOP (Scaffold Operating Platform)，图标库采用 `@icon-park/vue-next`，表格组件基于 Vxe-Table，采用 Monorepo + Git Submodule 架构 |
