# 实施计划

## 任务概览
[简述本功能的实施方法与整体策略，例如：采用分层架构，从数据模型 → 服务层 → API → 前端组件逐步构建，确保每层可独立测试与验证。]

## 指导文档合规性
[说明任务如何遵循 structure.md 的文件组织约定与 tech.md 的技术模式，例如：所有模型文件置于 src/models/，服务实现继承 BaseService，前端组件使用 React Hooks 与项目统一主题样式。]

## 原子化任务要求
**为确保代理高效执行，每个任务必须满足以下标准：**
- **文件范围**：最多涉及 1–3 个相关文件
- **时间限定**：经验开发者可在 15–30 分钟内完成
- **单一目标**：每项任务仅产生一个可测试的结果
- **明确文件**：必须指定需创建或修改的确切文件路径
- **代理友好**：输入/输出清晰，上下文切换最少

## 任务格式规范
- 使用复选框格式：`- [ ] 任务编号. 任务描述`
- **指定文件**：始终包含需创建/修改的完整文件路径
- **包含实现细节**：以子项形式列出关键实现点
- 引用需求使用：`_需求：X.Y, Z.A_`
- 引用可复用代码使用：`_复用：path/to/file.ts, path/to/component.tsx_`
- 仅聚焦编码任务（不含部署、用户测试等）
- **避免宽泛术语**：任务标题中不得使用“系统”、“集成”、“完整”等模糊词汇

## 优秀任务 vs 不良任务示例
❌ **不良示例（过于宽泛）**：
- “实现认证系统”（影响多个文件，多目标）
- “添加用户管理功能”（范围模糊，未指定文件）
- “构建完整仪表盘”（规模过大，含多个组件）

✅ **优秀示例（原子化）**：
- “在 models/user.py 中创建 User 模型，包含邮箱/密码字段”
- “在 utils/auth.py 中使用 bcrypt 添加密码哈希工具”
- “在 components/LoginForm.tsx 中创建 LoginForm 组件，含邮箱/密码输入框”

## 任务列表

- [ ] 1. 在 src/types/feature.ts 中创建核心接口
    - 文件：src/types/feature.ts
    - 定义功能所需 TypeScript 数据结构接口
    - 扩展自 base.ts 中的基类接口
    - 目的：为功能实现建立类型安全基础
    - _复用：src/types/base.ts_
    - _需求：1.1_

- [ ] 2. 在 src/models/FeatureModel.ts 中创建基础模型类
    - 文件：src/models/FeatureModel.ts
    - 实现继承 BaseModel 的基础模型类
    - 使用现有验证工具添加验证方法
    - 目的：为功能提供数据层基础
    - _复用：src/models/BaseModel.ts, src/utils/validation.ts_
    - _需求：2.1_

- [ ] 3. 在 FeatureModel.ts 中添加具体模型方法
    - 文件：src/models/FeatureModel.ts（延续任务2）
    - 实现 create、update、delete 方法
    - 添加外键关系处理逻辑
    - 目的：完成模型的 CRUD 功能
    - _复用：src/models/BaseModel.ts_
    - _需求：2.2, 2.3_

- [ ] 4. 在 tests/models/FeatureModel.test.ts 中创建模型单元测试
    - 文件：tests/models/FeatureModel.test.ts
    - 编写模型验证与 CRUD 方法测试
    - 使用现有测试工具与模拟数据
    - 目的：确保模型可靠性，防止回归问题
    - _复用：tests/helpers/testUtils.ts, tests/fixtures/data.ts_
    - _需求：2.1, 2.2_

- [ ] 5. 在 src/services/IFeatureService.ts 中创建服务接口
    - 文件：src/services/IFeatureService.ts
    - 定义含方法签名的服务契约
    - 扩展基础服务接口模式
    - 目的：为依赖注入建立服务层契约
    - _复用：src/services/IBaseService.ts_
    - _需求：3.1_

- [ ] 6. 在 src/services/FeatureService.ts 中实现功能服务
    - 文件：src/services/FeatureService.ts
    - 使用 FeatureModel 创建具体服务实现
    - 使用现有错误工具添加错误处理
    - 目的：为功能操作提供业务逻辑层
    - _复用：src/services/BaseService.ts, src/utils/errorHandler.ts, src/models/FeatureModel.ts_
    - _需求：3.2_

- [ ] 7. 在 src/utils/di.ts 中添加服务依赖注入
    - 文件：src/utils/di.ts（修改现有文件）
    - 在依赖注入容器中注册 FeatureService
    - 配置服务生命周期与依赖项
    - 目的：支持应用内服务注入
    - _复用：src/utils/di.ts 中现有 DI 配置_
    - _需求：3.1_

- [ ] 8. 在 tests/services/FeatureService.test.ts 中创建服务单元测试
    - 文件：tests/services/FeatureService.test.ts
    - 编写带模拟依赖的服务方法测试
    - 测试错误处理场景
    - 目的：确保服务可靠性与正确错误处理
    - _复用：tests/helpers/testUtils.ts, tests/mocks/modelMocks.ts_
    - _需求：3.2, 3.3_

---

⚠️ **以下任务编号存在重复或结构错误，需修正以符合原子化原则：**

> ❗ 原始任务编号 4、5、6 下存在子任务 4.1、4.2、5.1、5.2、6.1、6.2 —— 这违反了“原子任务编号唯一性”与“避免层级嵌套”的最佳实践。建议拆分为独立顶级任务，并重新编号。

---

✅ **修正后建议任务结构（续接任务8之后）：**

- [ ] 9. 创建 API 路由结构（src/routes/featureRoutes.ts）
    - 文件：src/routes/featureRoutes.ts
    - 定义功能相关路由路径
    - _复用：src/api/baseApi.ts, src/utils/apiUtils.ts_
    - _需求：4.0_

- [ ] 10. 设置路由中间件（src/middleware/featureMiddleware.ts）
    - 文件：src/middleware/featureMiddleware.ts
    - 配置身份验证与错误处理中间件
    - _复用：src/middleware/auth.ts, src/middleware/errorHandler.ts_
    - _需求：4.1_

- [ ] 11. 实现 CRUD API 端点（src/controllers/FeatureController.ts）
    - 文件：src/controllers/FeatureController.ts
    - 实现 GET/POST/PUT/DELETE 接口
    - 添加请求体验证逻辑
    - _复用：src/controllers/BaseController.ts, src/utils/validation.ts_
    - _需求：4.2, 4.3_

- [ ] 12. 编写 API 集成测试（tests/integration/featureApi.test.ts）
    - 文件：tests/integration/featureApi.test.ts
    - 使用 Supertest 测试端到端 API 行为
    - 验证状态码、响应结构与错误处理
    - _复用：tests/helpers/testUtils.ts, tests/fixtures/data.ts_
    - _需求：4.2, 4.3_

- [ ] 13. 创建基础 UI 组件（src/components/feature/BaseFeatureCard.tsx）
    - 文件：src/components/feature/BaseFeatureCard.tsx
    - 实现可复用卡片组件，支持主题样式
    - _复用：src/components/BaseComponent.tsx, src/styles/theme.ts_
    - _需求：5.1_

- [ ] 14. 实现功能专属组件（src/components/feature/FeatureList.tsx）
    - 文件：src/components/feature/FeatureList.tsx
    - 使用 useApi Hook 获取数据并渲染列表
    - 添加加载/错误状态处理
    - _复用：src/hooks/useApi.ts, src/components/BaseComponent.tsx_
    - _需求：5.2, 5.3_

- [ ] 15. 编写端到端测试（tests/e2e/featureJourney.test.ts）
    - 文件：tests/e2e/featureJourney.test.ts
    - 使用 Cypress/Playwright 模拟用户完整操作流程
    - 覆盖“创建 → 查看 → 编辑 → 删除”核心路径
    - _复用：tests/helpers/testUtils.ts, tests/fixtures/data.ts_
    - _需求：全部_

- [ ] 16. 最终集成与代码清理
    - 整合所有模块，确保端到端流程畅通
    - 修复跨模块类型或接口不匹配问题
    - 清理临时代码、补充注释、更新文档
    - _复用：src/utils/cleanup.ts, docs/templates/feature.md_
    - _需求：全部_

---

📌 **实施建议**：
- 请按顺序执行任务，前序任务未完成前不启动后续任务
- 每完成一项任务，立即运行 `claude-code-spec-workflow get-tasks {feature-name} {task-id} --mode complete`
- 执行下一项任务前，务必等待用户明确指令
- 所有任务完成后，运行 `/spec-status {feature-name}` 确认整体进度

✅ 本计划已按原子化、可执行、可追溯原则重构，确保与spec驱动工作流完美兼容。
