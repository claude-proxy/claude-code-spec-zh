# Claude Code Spec 工作流

> **⚠️ 重要通知：** 开发重心已转移至本工作流系统的 **MCP（Model Context Protocol）版本**。MCP 版本提供增强功能、实时仪表盘以及更广泛的 AI 工具兼容性。
>
> **🚀 [查看全新的 Spec 工作流 MCP →](https://github.com/Pimzino/spec-workflow-mcp)**
>
> 此专为 Claude Code 设计的版本仍可供现有用户使用，但将仅获得有限的更新。

[![npm version](https://badge.fury.io/js/@pimzino%2Fclaude-code-spec-workflow.svg?cacheSeconds=300)](https://badge.fury.io/js/@pimzino%2Fclaude-code-spec-workflow)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**为 Claude Code 提供自动化工作流与智能任务执行。**

通过结构化的工作流革新您的开发流程：新功能采用 **需求 → 设计 → 任务 → 实施**，bug修复则采用简化的 **报告 → 分析 → 修复 → 验证**。

## ☕ 支持本项目

<a href="https://buymeacoffee.com/Pimzino" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>

---

## 📦 安装

1. 全局安装工作流
```bash
npm i -g @pimzino/claude-code-spec-workflow
```
2. 在您的项目目录中运行设置命令
```bash
claude-code-spec-workflow
```
**搞定，您已准备就绪！**
---

## ✨ 您将获得

- **📁 完整的 .claude/ 目录结构** - 包含所有文件和目录
- **📝 10 个斜杠命令** - 5 个 spec 工作流 + 5 个bug修复工作流
- **🎯 智能任务执行** - 自动化实施
- **🤖 4 个专用代理** - 增强自动化
- **📊 实时仪表盘** - 可视化监控进度
- **🔧 自动生成命令** - 每项任务对应一个命令
- **📋 文档模板** - 专业的 spec 文档
- **⚙️ 项目引导** - 持久的上下文和标准
- **⚡ 智能优化** - 智能上下文共享和缓存

---

## 🔄 工作流概览

### 📊 **Spec 工作流** (新功能)

**一条命令实现完全自动化：**

```bash
/spec-create feature-name "描述"
```

**执行过程：**
1. **需求** → 用户故事 + 验收标准
2. **设计** → 技术架构 + 图表
3. **任务** → 原子化、适合代理执行的分解
4. **命令** → 自动生成任务命令（可选）

**执行任务：**
```bash
# 手动控制
/spec-execute 1 feature-name
/feature-name-task-1        # 自动生成
```

### 🐛 **bug修复工作流** (快速修复)

```bash
/bug-create issue-name "描述"  # 以结构化格式记录bug
/bug-analyze                          # 查找根本原因
/bug-fix                             # 实施解决方案
/bug-verify                          # 确认修复
```

### 🎯 **引导设置** (项目上下文)

```bash
/spec-steering-setup  # 创建 product.md, tech.md, structure.md
```

---

## 🛠️ 命令参考

<details>
<summary><strong>📊 Spec 工作流命令</strong></summary>

| 命令 | 用途 |
|---------|---------|
| `/spec-steering-setup` | 创建项目上下文文档 |
| `/spec-create <name>` | 完整的 spec 工作流 |
| `/spec-execute <task-id>` | 手动执行任务 |
| `/<name>-task-<id>` | 自动生成的任务命令 |
| `/spec-status` | 显示进度 |
| `/spec-list` | 列出所有 specs |

</details>

<details>
<summary><strong>🐛 bug修复命令</strong></summary>

| 命令 | 用途 |
|---------|---------|
| `/bug-create <name>` | 以结构化格式记录bug |
| `/bug-analyze` | 调查根本原因 |
| `/bug-fix` | 实施针对性解决方案 |
| `/bug-verify` | 验证修复 |
| `/bug-status` | 显示bug修复进度 |

</details>

---

## 🎯 核心特性

### 🤖 **智能任务执行**
- **简化**的任务实施
- **上下文感知**的执行，具备完整的规格上下文
- **基于代理**的实施，使用 spec-task-executor

### 🧠 **专用代理** (可选)
4 个用于增强自动化的 AI 代理：

**核心工作流：** `spec-task-executor`, `spec-requirements-validator`, `spec-design-validator`, `spec-task-validator`


> **注意：** 代理是可选的 —— 即使没有代理，所有功能也能通过内置回退机制正常工作。

### ⚡ **完整的上下文优化** (新增!)
- **通用上下文共享** - 优化引导、规格和模板文档
- **60-80% 的 token 减少** - 消除所有文档类型中冗余的文档获取
- **三重优化命令** - `get-steering-context`, `get-spec-context`, 和 `get-template-context`
- **智能文档处理** - bug文档使用直接读取（无冗余），模板使用批量加载（高冗余）
- **性能提升** - 通过跨所有工作流的缓存上下文实现更快的代理执行
- **自动回退** - 在优化不可用时，通过单个 `get-content` 保持可靠性
- **基于会话的缓存** - 智能文件变更检测和缓存失效

### 📊 **实时仪表盘**
```bash
npx -p @pimzino/claude-code-spec-workflow claude-spec-dashboard
```
- 实时进度跟踪
- WebSocket 更新
- Git 集成
- 使用 Tailwind CSS 的现代化 UI

---

### 🔗 仪表盘隧道 (新增!)

通过临时 HTTPS URL 安全地与外部利益相关者分享您的仪表盘：

```bash
# 启动带隧道的仪表盘
npx -p @pimzino/claude-code-spec-workflow claude-spec-dashboard --tunnel

# 带密码保护
npx -p @pimzino/claude-code-spec-workflow claude-spec-dashboard --tunnel --tunnel-password mySecret123

# 选择特定提供商
npx -p @pimzino/claude-code-spec-workflow claude-spec-dashboard --tunnel --tunnel-provider cloudflare
```

**隧道特性：**
- **🔒 安全的 HTTPS URL** - 与经理、客户或远程团队成员分享仪表盘
- **👁️ 只读访问** - 外部查看者无法修改任何项目数据
- **🔑 可选密码** - 使用密码认证保护访问
- **🌐 多提供商支持** - 在 Cloudflare 和 ngrok 之间自动回退
- **📊 使用分析** - 跟踪谁在何时访问了您的仪表盘
- **⏰ 自动过期** - 当您停止仪表盘时，隧道自动关闭
- **🚀 零配置** - 开箱即用，内置提供商支持

## 📊 命令行选项

### 设置命令
```bash
# 在当前目录设置
npx @pimzino/claude-code-spec-workflow

# 在指定目录设置
npx @pimzino/claude-code-spec-workflow --project /path/to/project

# 强制覆盖现有文件
npx @pimzino/claude-code-spec-workflow --force

# 跳过确认提示
npx @pimzino/claude-code-spec-workflow --yes

# 测试设置
npx @pimzino/claude-code-spec-workflow test
```

### 仪表盘命令
```bash
# 基础仪表盘
npx -p @pimzino/claude-code-spec-workflow claude-spec-dashboard

# 带隧道的仪表盘（外部共享）
npx -p @pimzino/claude-code-spec-workflow claude-spec-dashboard --tunnel

# 完整的隧道配置
npx -p @pimzino/claude-code-spec-workflow claude-spec-dashboard \
  --tunnel \
  --tunnel-password mySecret123 \
  --tunnel-provider cloudflare \
  --port 3000 \
  --open
```

## 🎯 引导文档 (新增!)

引导文档提供持久的项目上下文，指导所有 spec 开发：

### **产品文档** (`product.md`)
- 产品愿景和目的
- 目标用户及其需求
- 关键功能和目标
- 成功指标

### **技术文档** (`tech.md`)
- 技术栈和框架
- 开发工具和实践
- 技术约束和要求
- 第三方集成

### **结构文档** (`structure.md`)
- 文件组织模式
- 命名约定
- 导入模式
- 代码组织原则

运行 `/spec-steering-setup` 来创建这些文档。Claude 将分析您的项目并帮助您定义这些标准。

## 🎨 特性

### ✅ **零配置**
- 开箱即用，适用于任何项目
- 自动检测项目类型（Node.js, Python, Java 等）
- 验证 Claude Code 安装

### ✅ **交互式设置**
- 带有进度指示器的精美 CLI
- 用于安全的确认提示
- 有用的错误消息和指导

### ✅ **智能文件管理**
- 每个命令文件中包含完整的工作流说明
- 创建全面的目录结构
- 包含所有必要的模板和配置

### ✅ **专业品质**
- **完整的 TypeScript 实现**，具有严格的类型检查
- **前端转换为 TypeScript**，以增强仪表盘开发
- **95%+ 的类型覆盖率**，无隐式 any 类型
- **现代化的构建管道**，支持 esbuild 打包和源映射
- 全面的错误处理
- 遵循 npm 最佳实践

### ✅ **引导文档集成**
- 跨所有 specs 的持久项目上下文
- 自动与项目标准对齐
- 一致的代码生成
- 减少重复解释的需求

### ✅ **TypeScript 仪表盘前端**
- **类型安全的前端代码**，具有全面的接口
- **实时 WebSocket 通信**，具有类型化的消息处理
- **Petite-vue 集成**，具有自定义类型定义
- **构建管道**，支持开发和生产包
- **严格的空值检查** 和现代化的 TypeScript 模式
- **JSDoc 文档**，涵盖所有导出的函数

## 🏗️ 设置后的项目结构

```
your-project/
├── .claude/
│   ├── commands/           # 14 个斜杠命令 + 自动生成
│   ├── steering/          # product.md, tech.md, structure.md
│   ├── templates/         # 文档模板
│   ├── specs/            # 生成的规格
│   ├── bugs/             # bug修复工作流
│   └── agents/           # AI 代理（默认启用）
```

## 🧪 测试

该包包含一个内置的测试命令：

```bash
# 在临时目录中测试设置
npx @pimzino/claude-code-spec-workflow test
```

## 📋 要求

- **Node.js** 16.0.0 或更高版本
- **Claude Code** 已安装并配置
- 任何项目目录

## 🔧 故障排除

### 常见问题

**❓ NPX 后找不到命令**
```bash
# 确保您使用了正确的包名
npx @pimzino/claude-code-spec-workflow
```

**❓ 设置因权限错误失败**
```bash
# 尝试使用不同的目录权限
npx @pimzino/claude-code-spec-workflow --project ~/my-project
```

**❓ 未检测到 Claude Code**
```bash
# 首先安装 Claude Code
npm install -g @anthropic-ai/claude-code
```

### 调试信息

```bash
# 显示详细输出
DEBUG=* npx @pimzino/claude-code-spec-workflow

# 检查包版本
npx @pimzino/claude-code-spec-workflow --version
```

## 🌟 示例

### 基本用法
```bash
cd my-awesome-project
npx @pimzino/claude-code-spec-workflow
claude
# 输入： /spec-create user-dashboard "用户资料管理"
```

### 高级用法
```bash
# 设置多个项目
for dir in project1 project2 project3; do
  npx @pimzino/claude-code-spec-workflow --project $dir --yes
done
```

## 🔧 TypeScript 开发

### 前端仪表盘开发

仪表盘前端完全使用 TypeScript 实现，以增强类型安全性和开发者体验：

#### 类型定义
```typescript
// 核心仪表盘类型
interface Project {
  path: string;
  name: string;
  level: number;
  hasActiveSession: boolean;
  specs: Spec[];
  bugs: Bug[];
  steeringStatus?: SteeringStatus;
}

// WebSocket 消息类型，使用可区分联合
type WebSocketMessage = 
  | { type: 'initial'; data: InitialData }
  | { type: 'update'; data: UpdateData }
  | { type: 'error'; data: ErrorData }
  | { type: 'tunnel-status'; data: TunnelStatusData };
```

#### 构建命令
```bash
# TypeScript 编译和打包
npm run build:frontend:dev   # 为开发构建前端
npm run build:frontend:prod  # 为生产构建前端（压缩）
npm run watch:frontend       # 监听模式，自动重建
npm run typecheck:frontend   # 仅类型检查（无输出）
npm run typecheck           # 检查后端和前端类型

# 开发工作流  
npm run dev:dashboard       # 启动带热重载的仪表盘（前端 + 后端）
npm run dev:dashboard:backend-only  # 仅启动后端（用于前端调试）

# 完整构建流程
npm run build              # 完整构建：TypeScript + 前端 + 静态文件
npm run lint               # 使用自动修复功能检查 TypeScript 文件
npm run format             # 使用 Prettier 格式化代码
```

#### 类型安全特性
- **严格的 TypeScript 配置**，包含空值检查
- **运行时类型验证**，使用类型守卫
- **WebSocket 消息类型化**，用于实时更新
- **状态管理类型**，用于响应式 UI 组件
- **错误处理类型**，使用 Result<T> 模式
- **Petite-vue 集成**，具有自定义类型定义

#### 类型使用示例

```typescript
// 导入仪表盘类型
import type { Project, WebSocketMessage, AppState } from './dashboard.types';

// 类型安全的项目处理
function selectProject(project: Project): void {
  console.log(`Selected: ${project.name} (${project.specs.length} specs)`);
  
  // 使用可选链进行安全属性访问
  const steeringCount = project.steeringStatus?.totalDocs ?? 0;
  if (steeringCount > 0) {
    console.log(`Steering docs: ${steeringCount}`);
  }
}

// 使用可区分联合的 WebSocket 消息处理
function handleMessage(message: WebSocketMessage): void {
  switch (message.type) {
    case 'initial':
      // TypeScript 知道 data 是 InitialData
      console.log(`Loaded ${message.data.projects.length} projects`);
      break;
    case 'update':
      // TypeScript 知道 data 是 UpdateData
      console.log(`Updated project: ${message.data.projectPath}`);
      break;
    case 'error':
      // TypeScript 知道 data 是 ErrorData
      console.error(`Error: ${message.data.message}`);
      break;
  }
}

// 运行时验证的类型守卫
function isValidProject(obj: unknown): obj is Project {
  return (
    typeof obj === 'object' &&
    obj !== null &&
    'path' in obj &&
    'name' in obj &&
    'specs' in obj &&
    Array.isArray((obj as Project).specs)
  );
}

// 用于错误处理的 Result 类型
type Result<T, E = Error> = 
  | { success: true; data: T }
  | { success: false; error: E };

function parseProjectData(data: unknown): Result<Project> {
  if (isValidProject(data)) {
    return { success: true, data };
  }
  return { success: false, error: new Error('Invalid project data') };
}
```

#### 开发指南
- **所有导出函数都包含 JSDoc 文档**
- **保持 95%+ 的类型覆盖率**（无隐式 any 类型）
- **现代 TypeScript 模式**（可选链、空值合并）
- **优先使用类型守卫**，而非类型断言
- **对象形状使用接口**，可区分联合使用联合类型
- **错误处理使用 Result<T> 模式**
- **使用类型守卫进行运行时验证**，处理外部数据

## 📚 文档

- **[完整文档](https://github.com/pimzino/claude-code-spec-workflow#readme)**
- **[隧道功能指南](./docs/tunnel-feature.md)** - 全面的隧道文档
- **[隧道示例](./examples/tunnel/)** - 即用型隧道脚本
- **[Claude Code 文档](https://docs.anthropic.com/claude-code)**
- **[TypeScript API 参考](./docs/typescript-api.md)** - 从 JSDoc 注释生成

## 🤝 贡献

欢迎贡献！请参阅我们的 [贡献指南](https://github.com/pimzino/claude-code-spec-workflow/blob/main/CONTRIBUTING.md)。

## 📄 许可证

MIT 许可证 - 详情见 [LICENSE](https://github.com/pimzino/claude-code-spec-workflow/blob/main/LICENSE)。

## 🏷️ 变更日志

版本历史请见 [CHANGELOG.md](https://github.com/pimzino/claude-code-spec-workflow/blob/main/CHANGELOG.md)。

---

## 🚦 何时使用何种方法

| 场景 | 推荐方法 |
|----------|---------------------|
| **定义明确的新功能** | `/spec-execute` 或单个任务命令 |
| **复杂/实验性功能** | `/spec-execute`（手动控制） |
| **现有代码中的bug** | bug工作流 (`/bug-create` → `/bug-verify`) |
| **学习代码库** | 使用单个命令手动执行 |
| **生产部署** | 完整的 spec 工作流，附带完成审查 |

---

## 🚀 安装与设置

### **安装**
```bash
# 全局安装（推荐）
npm install -g @pimzino/claude-code-spec-workflow

# 验证安装
claude-code-spec-workflow --version
```

### **设置选项**
```bash
# 基础设置
claude-code-spec-workflow

# 高级选项
claude-code-spec-workflow --project /path --force --yes
```

**设置过程中您将选择：**
- ✅ **启用代理？** 增强自动化 vs 更简单的设置
- ✅ **项目分析** 自动检测框架和模式

---

## 📚 示例
**建议：使用 Claude Opus 4 生成 spec 文档 '/spec-create'，然后使用 Claude Sonnet 4 进行实施，即 '/spec-execute' 或 '/{spec-name}-task-<id>'。**
<details>
<summary><strong>基础工作流示例</strong></summary>

```bash
# 1. 全局安装（一次）
npm install -g @pimzino/claude-code-spec-workflow

# 2. 设置项目（一次）
cd my-project
claude-code-spec-workflow

# 3. 创建引导文档（推荐）
claude
/spec-steering-setup

# 4. 创建功能 spec
/spec-create user-authentication "安全登录系统"

# 5. 执行任务
/spec-execute 1 user-authentication

# 6. 监控进度
/spec-status user-authentication
```

</details>

<details>
<summary><strong>bug修复示例</strong></summary>

```bash
/bug-create login-timeout "用户注销过快"
/bug-analyze
/bug-fix
/bug-verify
```

</details>

---

## ⚡ 上下文优化命令

该包包含用于高效加载所有文档类型的优化命令：

### **get-steering-context**
一次性加载所有引导文档以共享上下文：
```bash
claude-code-spec-workflow get-steering-context
```
**输出**: 格式化的 markdown，包含所有引导文档 (product.md, tech.md, structure.md)

### **get-spec-context**
一次性加载所有规格文档以共享上下文：
```bash
claude-code-spec-workflow get-spec-context feature-name
```
**输出**: 格式化的 markdown，包含所有规格文档 (requirements.md, design.md, tasks.md)

### **get-template-context**
按类别加载模板以共享上下文：
```bash
# 加载所有模板
claude-code-spec-workflow get-template-context

# 加载特定模板类别
claude-code-spec-workflow get-template-context spec    # Spec 模板
claude-code-spec-workflow get-template-context bug     # bug模板
claude-code-spec-workflow get-template-context steering # 引导模板
```
**输出**: 格式化的 markdown，包含请求的模板

### **智能文档处理**
- **高冗余文档** (引导、规格、模板): 使用优化的批量加载
- **低冗余文档** (bug报告): 使用直接文件读取以简化
- **选择性委托**: 主代理加载完整上下文，但仅向子代理传递相关部分
- **单个文件**: 继续使用 `get-content` 处理边缘情况

### **优势**
- **相比单个文件加载，减少 60-80% 的 token**
- **通过跨所有工作流的缓存上下文实现更快执行**
- **需要时自动回退到单个 `get-content`**
- **基于会话的缓存**，具备智能文件变更检测

### **分层上下文管理**
系统实现了复杂的**分层上下文管理策略**，以实现最高效率：

**主代理** (如 `/spec-execute`, `/spec-create` 等命令):
- **开始时一次性加载所有上下文**，使用优化命令
- **存储完整上下文**，用于任务协调和决策
- **向子代理分发选择性上下文**，无需重新加载

**子代理** (如 `spec-task-executor` 等代理):
- **优先级 1**: 使用任务说明中提供的上下文（引导、规格、任务详情）
- **优先级 2**: 如果上述未提供，则回退到加载上下文
- **从不冗余加载** 已由主代理提供的上下文

**上下文分发模式**:
```
主代理加载: 引导 + 完整规格 + 任务详情
↓ 委托给子代理，包含:
├── 完整的引导上下文
├── 选择性规格上下文（仅需求 + 设计）
├── 特定任务详情
└── 明确指示: "请勿重新加载上下文"
```

此方法**消除了冗余加载**，同时确保每个代理都拥有其所需的精确上下文。

---

## 🛟 故障排除

<details>
<summary><strong>常见问题</strong></summary>

**❓ “命令未找到”**
```bash
# 首先全局安装
npm install -g @pimzino/claude-code-spec-workflow

# 然后使用命令
claude-code-spec-workflow
```

**❓ “未检测到 Claude Code”**
```bash
npm install -g @anthropic-ai/claude-code
```

**❓ “权限错误”**
```bash
claude-code-spec-workflow --project ~/my-project
```

</details>

---

## 📋 要求

- **Node.js** 16.0.0+
- **Claude Code** 已安装
- 任何项目目录

---

## 🔗 链接

- **[完整文档](https://github.com/pimzino/claude-code-spec-workflow#readme)**
- **[Claude Code 文档](https://docs.anthropic.com/claude-code)**
- **[报告问题](https://github.com/pimzino/claude-code-spec-workflow/issues)**

---

## 📄 许可证与致谢

**MIT 许可证** - [LICENSE](LICENSE)

**由 [Pimzino](https://github.com/pimzino) 倾情制作 ❤️**

**特别感谢:**
- @pimzino - 初始设置
- @boundless-oss - 引导文档
- @mquinnv - 仪表盘功能

**技术支持：** [Claude Code](https://docs.anthropic.com/claude-code) • [Mermaid](https://mermaid.js.org/) • [TypeScript](https://www.typescriptlang.org/)