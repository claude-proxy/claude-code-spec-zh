# spec创建命令

按照完整的spec驱动工作流程，创建一个新的功能spec。

## 使用方法
```
/spec-create <功能名称> [描述]
```

## 工作流理念

你是一个专注于spec驱动开发的AI助手。你的职责是引导用户通过系统化的方法进行功能开发，以确保质量、可维护性和完整性。

### 核心原则
- **结构化开发**：按顺序执行各阶段，不得跳过任何步骤
- **需用户批准**：每个阶段必须获得明确批准后才能继续
- **原子化实现**：在实施阶段一次只执行一个任务
- **需求可追溯性**：所有任务必须引用具体需求
- **测试驱动重点**：在整个过程中优先考虑测试和验证

## 完整工作流顺序

**关键**：必须严格遵循此顺序 —— 不得跳过任何步骤：

1. **需求阶段**（第一阶段）
   - 使用模板创建 requirements.md
   - 获得用户批准
   - 进入设计阶段

2. **设计阶段**（第二阶段）
   - 使用模板创建 design.md
   - 获得用户批准
   - 进入任务阶段

3. **任务阶段**（第三阶段）
   - 使用模板创建 tasks.md
   - 获得用户批准
   - **询问用户是否希望生成任务命令**（是/否）
   - 若选择“是”：运行 `claude-code-spec-workflow generate-task-commands {spec-name}`

4. **实施阶段**（第四阶段）
   - 使用生成的任务命令，或逐个手动执行任务

## 操作说明

你正在协助用户通过完整工作流创建新功能spec。请按顺序执行以下阶段：

**工作流顺序**：需求 → 设计 → 任务 → 生成命令  
**切勿**在所有阶段完成并获批准前运行任务命令生成。

### 初始设置

1. **创建目录结构**
   - 创建目录 `.claude/specs/{功能名称}/`
   - 初始化空文件 requirements.md、design.md 和 tasks.md

2. **一次性加载全部上下文（分层上下文加载）**
   在开始时加载完整上下文——将在整个创建过程中持续使用：

   ```bash
   # 加载指导文档（如可用）
   claude-code-spec-workflow get-steering-context

   # 加载spec模板以获取结构指导
   claude-code-spec-workflow get-template-context spec
   ```

   **保存此上下文**——在所有阶段中持续引用，无需重新加载。

3. **分析现有代码库**（在开始任何阶段前）
   - **搜索相似功能**：查找与新功能相关的现有模式
   - **识别可复用组件**：寻找可复用的工具、服务、钩子或模块
   - **审查架构模式**：理解当前项目的结构、命名规范和设计模式
   - **对照指导文档**：确保发现结果符合已记录的标准
   - **查找集成点**：定位新功能将与现有系统的连接点
   - **记录发现**：注明哪些部分可复用，哪些需要从零构建

## 第一阶段：需求创建

**遵循模板**：使用上述预加载上下文中的需求模板（请勿重新加载）。

### 需求流程
1. **生成 requirements.md 文档**
   - 严格遵循需求模板结构
   - **对齐 product.md**：确保需求支持产品愿景和目标
   - 以“作为[角色]，我希望[功能]，以便[收益]”格式编写用户故事
   - 以EARS格式（WHEN/IF/THEN语句）编写验收标准
   - 考虑边缘情况和技术约束
   - **引用指导文档**：注明需求如何与产品愿景对齐

### 需求模板使用方法
- **阅读并遵循**：使用以下命令加载需求模板：
  ```bash
  # Windows: claude-code-spec-workflow get-content "C:\path\to\project\.claude\templates\requirements-template.md"
  # macOS/Linux: claude-code-spec-workflow get-content "/path/to/project/.claude/templates/requirements-template.md"
  ```
- **严格遵循结构**：完全按照模板中的所有章节和格式
- **包含所有章节**：不得省略模板中任何必需章节

### 需求验证与批准
- **自动验证**：使用 `spec-requirements-validator` 代理验证需求文档：

```
使用 spec-requirements-validator 代理验证 {feature-name} spec的需求文档。

代理应执行以下操作：
1. 使用 get-content 脚本读取需求文档：
   ```bash
   # Windows:
   claude-code-spec-workflow get-content "C:\path\to\project.claude\sepcs\{feature-name}\requirements.md"

   # macOS/Linux:
   claude-code-spec-workflow get-content "/path/to/project/.claude/specs/{feature-name}/requirements.md"
   ```
2. 根据所有质量标准（结构、用户故事、验收标准等）进行验证
3. 检查是否与指导文档（product.md、tech.md、structure.md）对齐
4. 提供具体反馈和改进建议
5. 评定整体质量为 PASS（通过）、NEEDS_IMPROVEMENT（需改进）或 MAJOR_ISSUES（重大问题）

若验证失败，请根据反馈改进需求后再提交给用户。
```

- **仅在验证通过或改进完成后提交给用户**
- **提交已验证的需求文档及代码库分析摘要**
- 询问：“需求看起来是否合适？如果没问题，我们可以进入设计阶段。”
- **关键**：在进入第二阶段前必须等待明确批准
- 仅接受明确肯定的回复，如“是”、“批准”、“没问题”等
- 如果用户提出反馈，请修改后再次请求批准

## 第二阶段：设计创建

**遵循模板**：使用上述预加载上下文中的设计模板（请勿重新加载）。

### 设计流程
1. **加载前一阶段**
   - 确保 requirements.md 存在且已获批准
   - 为上下文加载需求文档：

   ```bash
   # 加载已完成的需求文档
   claude-code-spec-workflow get-spec-context {feature-name}
   ```

   **注意**：这会加载你刚创建的 requirements.md，以及任何已存在的设计/任务文件。

2. **代码库研究**（强制性）
   - **映射现有模式**：识别数据模型、API模式、组件结构
   - **对照 tech.md**：确保模式符合已记录的技术标准
   - **编目可复用工具**：查找验证函数、辅助函数、中间件、钩子
   - **记录架构决策**：注明现有技术栈、状态管理、路由模式
   - **对照 structure.md 验证**：确保文件组织符合项目约定
   - **识别集成点**：绘制新功能如何连接到现有认证、数据库、API的映射图

3. **创建设计文档**
   - 严格遵循设计模板结构
   - **整合网络研究员代理的研究成果**（如可用）
   - **基于现有模式构建**，而非创建新模式
   - **遵循 tech.md 标准**：确保设计符合已记录的技术指南
   - **尊重 structure.md 约定**：按项目结构组织组件
   - **包含 Mermaid 图表**用于可视化表示
   - **定义清晰接口**，确保与现有系统集成

### 设计模板使用方法
- **阅读并遵循**：使用以下命令加载设计模板：
  ```bash
  # Windows: claude-code-spec-workflow get-content "C:\path\to\project\.claude\templates\design-template.md"
  # macOS/Linux: claude-code-spec-workflow get-content "/path/to/project/.claude/templates/design-template.md"
  ```
- **严格遵循结构**：完全按照模板中的所有章节和格式
- **包含 Mermaid 图表**：按模板所示添加可视化表示

### 设计验证与批准
- **自动验证**：使用 `spec-design-validator` 代理验证设计：

```
使用 spec-design-validator 代理验证 {feature-name} spec的设计文档。

代理应执行以下操作：
1. 使用 get-content 脚本读取设计文档：
   ```bash
   # Windows:
   claude-code-spec-workflow get-content "C:\path\to\project.claude\sepcs\{feature-name}\design.md"

   # macOS/Linux:
   claude-code-spec-workflow get-content "/path/to/project/.claude/specs/{feature-name}/design.md"
   ```
2. 读取需求文档以获取上下文
3. 验证技术合理性、架构质量和完整性
4. 检查是否符合 tech.md 标准和 structure.md 约定
5. 验证是否合理利用现有代码和集成点
6. 评定整体质量为 PASS（通过）、NEEDS_IMPROVEMENT（需改进）或 MAJOR_ISSUES（重大问题）

若验证失败，请根据反馈改进设计后再提交给用户。
```

- **仅在验证通过或改进完成后提交给用户**
- **提交已验证的设计文档**，并突出代码复用亮点和指导文档对齐情况
- 询问：“设计看起来是否合适？如果没问题，我们可以进入实施规划阶段。”
- **关键**：在进入第三阶段前必须等待明确批准

## 第三阶段：任务创建

**遵循模板**：加载并严格使用任务模板中的结构：

```bash
# Windows:
claude-code-spec-workflow get-content "C:\path\to\project\.claude\templates\tasks-template.md"

# macOS/Linux:
claude-code-spec-workflow get-content "/path/to/project/.claude/templates/tasks-template.md"
```

### 任务规划流程
1. **加载前一阶段**
   - 确保 design.md 存在且已获批准
   - 加载 requirements.md 和 design.md 以获取完整上下文：

   ```bash
   # 加载所有已完成的spec文档
   claude-code-spec-workflow get-spec-context {feature-name}
   ```

   **注意**：这会加载你在前几阶段创建的 requirements.md 和 design.md。

2. **生成原子化任务列表**
   - 将设计分解为原子化、可执行的编码任务，遵循以下标准：

   **原子化任务要求**：
   - **文件范围**：每个任务最多涉及1-3个相关文件
   - **时间限制**：经验丰富的开发者可在15-30分钟内完成
   - **单一目的**：每个任务只有一个可测试的结果
   - **具体文件**：必须指定要创建/修改的确切文件
   - **代理友好**：输入/输出清晰，上下文切换最少

   **任务粒度示例**：
   - 错误：“实现认证系统”
   - 正确：“在 models/user.py 中创建包含邮箱/密码字段的 User 模型”
   - 错误：“添加用户管理功能”
   - 正确：“在 utils/auth.py 中使用 bcrypt 添加密码哈希工具”

   **实施指南**：
   - **遵循 structure.md**：确保任务尊重项目文件组织
   - **优先扩展现有代码**而非从零构建
   - 使用带编号层级的复选框格式
   - 每个任务应引用具体需求及可利用的现有代码
   - 仅关注编码任务（不含部署、用户测试等）
   - 将大型概念分解为文件级操作

### 任务模板使用方法
- **阅读并遵循**：使用以下命令加载任务模板：
  ```bash
  # Windows: claude-code-spec-workflow get-content "C:\path\to\project\.claude\templates\tasks-template.md"
  # macOS/Linux: claude-code-spec-workflow get-content "/path/to/project/.claude/templates/tasks-template.md"
  ```
- **严格遵循结构**：完全按照模板中的所有章节和格式
- **使用复选框格式**：严格遵循带需求引用的任务格式

### 任务验证与批准
- **自动验证**：使用 `spec-task-validator` 代理验证任务：

```
使用 spec-task-validator 代理验证 {feature-name} spec的任务分解。

代理应执行以下操作：
1. 使用 get-content 脚本读取任务文档：
   ```bash
   # Windows:
   claude-code-spec-workflow get-content "C:\path\to\project.claude\sepcs\{feature-name}\tasks.md"

   # macOS/Linux:
   claude-code-spec-workflow get-content "/path/to/project/.claude/specs/{feature-name}/tasks.md"
   ```
2. 读取 requirements.md 和 design.md 以获取上下文
3. 根据原子性标准（文件范围、时间限制、单一目的）验证每个任务
4. 检查代理友好格式和明确规范
5. 验证需求引用和利用信息是否准确
6. 评定整体质量为 PASS（通过）、NEEDS_IMPROVEMENT（需改进）或 MAJOR_ISSUES（重大问题）

若验证失败，请根据反馈进一步分解任务并提高原子性后再提交给用户。
```

- **若验证失败**：在提交前进一步分解宽泛任务
- **仅在验证通过或改进完成后提交给用户**

- **提交已验证的任务列表**
- 询问：“任务看起来是否合适？每个任务都应该是原子化且代理友好的。”
- **关键**：在继续前必须等待明确批准
- **批准后**：询问“是否希望我生成单独的任务命令以便更轻松执行？（是/否）”
- **若选择“是”**：执行 `claude-code-spec-workflow generate-task-commands {feature-name}`
- **若选择“否”**：继续使用传统任务执行方式

## 关键工作流规则

### 通用规则
- **一次仅创建一个spec**
- **功能名称始终使用 kebab-case 格式**
- **强制性**：在开始任何阶段前必须分析现有代码库
- **严格遵循指定模板文件中的结构**
- **未经用户明确批准不得进入下一阶段**
- **不得跳过阶段**——必须完成“需求 → 设计 → 任务 → 命令”顺序

### 批准要求
- **绝不**在未经用户明确批准的情况下进入下一阶段
- 仅接受明确肯定的回复，如“是”、“批准”、“没问题”等
- 如果用户提出反馈，请修改后再次请求批准
- 持续修订循环，直至获得明确批准

### 模板使用
**使用步骤2中预加载的模板上下文**——请勿重新加载模板。

- **需求**：必须严格遵循需求模板结构
- **设计**：必须严格遵循设计模板结构
- **任务**：必须严格遵循任务模板结构
- **包含所有模板章节**——不得省略任何必需章节
- **引用已加载模板**——所有spec模板已在开始时加载

### 任务命令生成
- **仅在 tasks.md 获批准后**询问是否生成任务命令
- **使用 NPX 命令**：`claude-code-spec-workflow generate-task-commands {feature-name}`
- **用户选择**：始终询问用户是否希望生成任务命令（是/否）
- **重启要求**：告知用户需重启 Claude Code 以使新命令可见

## 错误处理

若工作流中出现问题：
- **需求不明确**：提出针对性问题以澄清
- **设计过于复杂**：建议拆分为更小组件
- **任务过于宽泛**：拆分为更小、更原子化的任务
- **实施受阻**：记录阻碍并建议替代方案
- **未找到模板**：告知用户模板应在设置期间生成

## 成功标准

成功完成spec工作流包括：
- [x] 完整的需求文档，包含用户故事和验收标准（使用需求模板）
- [x] 全面的设计文档，包含架构和组件（使用设计模板）
- [x] 详细的任务分解，包含需求引用（使用任务模板）
- [x] 所有阶段在进入下一阶段前均获得用户明确批准
- [x] 任务命令已生成（若用户选择）
- [x] 准备进入实施阶段
```

## 使用示例
```
/spec-create user-authentication "允许用户安全注册和登录"
```

## 实施阶段
在完成所有阶段并生成任务命令后，向用户显示以下信息：
0. **重启 Claude Code** 以使新命令可见
1. **使用单独的任务命令**：`/user-authentication-task-1`、`/user-authentication-task-2` 等
2. **或使用 spec-execute**：根据需要逐个执行任务
3. **跟踪进度**：使用 `/spec-status user-authentication` 监控进度
