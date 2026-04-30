## 功能摘要：SOP (Scaffold Operating Platform) 前端框架

**核心需求**：打造一款基于 Vue3 生态的开箱即用后台管理二次开发框架 SOP，通过配置化组件、Hooks 封装、多套主题方案，帮助开发者快速搭建企业级后台系统。

**用户群体**：中高级前端开发者、需要快速交付后台管理系统的技术团队

**关键功能**：
- Must Have：
  - 项目脚手架（CLI 快速创建项目）`npm create sop`
  - 布局系统（上下/左右/混合布局）
  - 权限认证（登录/注册/JWT/角色权限）
  - VForm 配置化表单组件（基于 Element Plus）
  - VTable 配置化表格组件（基于 Vxe-Table）
- Should Have：
  - VUpload 上传组件、VEcharts 图表组件
  - 多套预设主题 + 在线主题定制工具
  - 按钮级权限控制（v-permission）
  - pc-template 模板工程（git submodule + pnpm workspace）

**技术栈**：Vue 3.3+ / Element Plus / Vxe-Table / Vite / Pinia / Vue Router / Vue I18n / Axios / @icon-park/vue-next / pnpm / git submodule

**验收标准数量**：5 个核心用户故事，35+ 条验收标准

**开放问题**：5 个待确认

---

## 项目架构

### Monorepo 结构

```
sop/                                    # SOP 主仓库
├── packages/
│   ├── lib/                              # 核心库 (@sop/lib)
│   │   ├── core/                         # 路由、状态、请求、权限等
│   │   └── components/                   # VForm、VTable(Vxe-Table)、Upload 等
│   ├── pages/                            # 业务页面库 (@sop/pages)
│   │   └── views/                        # 登录、注册、仪表盘、系统管理等
│   └── cli/                              # CLI 工具 (@sop/cli)
│       └── bin/sop.js
│
├── pc-template/                            # PC 端模板工程（独立仓库）
│   ├── packages/
│   │   ├── lib/                            # git submodule -> sop/packages/lib
│   │   └── pages/                            # git submodule -> sop/packages/pages
│   ├── play/                                 # 业务开发目录
│   ├── package.json                          # pnpm workspace 配置
│   └── pnpm-workspace.yaml
│
├── package.json
├── pnpm-workspace.yaml
└── README.md
```

---

## 里程碑（4 周）

| 阶段 | 周期 | 主要交付物 |
|-----|------|-----------|
| M1 基础设施 | Week 1 | CLI (@sop/cli)、packages/lib 核心库、工程化配置 |
| M2 核心组件 | Week 2 | VForm (Element Plus)、VTable (Vxe-Table) |
| M3 权限与高级组件 | Week 3 | 权限体系、Upload、Echarts |
| M4 模板、文档与发布 | Week 4 | pc-template、packages/pages、文档站点、npm 发布 |

---

## 建议后续步骤

1. **运行 `/ui-spec SOP`** → 生成交互设计规范
2. **运行 `/api-design SOP`** → 设计接口契约
3. **运行 `/test-plan SOP`** → 生成测试计划
4. **运行 `/sprint SOP`** → 拆解开发迭代计划
