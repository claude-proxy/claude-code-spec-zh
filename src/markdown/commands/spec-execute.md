# spec执行命令

执行已批准任务列表中的特定任务。

## 使用方法
```
/spec-execute [任务ID] [功能名称]
```

## 阶段概览
**你的角色**：系统化执行任务并进行验证

这是spec工作流的第四阶段。你的目标是逐个实现已批准任务列表中的各项任务。

## 操作说明

**执行步骤**：

**步骤1：加载上下文**
```bash
# 加载指导文档（如可用）
claude-code-spec-workflow get-steering-context

# 加载spec上下文
claude-code-spec-workflow get-spec-context {功能名称}

# 加载特定任务详情
claude-code-spec-workflow get-tasks {功能名称} {任务ID} --mode single
```

**步骤2：通过代理执行**
使用 `spec-task-executor` 代理：
```
请使用 spec-task-executor 代理为 {功能名称} spec实现任务 {任务ID}。

## 指导上下文
[在此粘贴 get-steering-context 命令的完整输出]

## spec上下文
[在此粘贴 get-spec-context 命令输出的需求和设计部分]

## 任务详情
[在此粘贴 get-tasks single 命令的输出]

## 指令
- 仅实现指定任务：{任务ID}
- 遵循所有项目约定并复用现有代码
- 使用以下命令将任务标记为完成：
  claude-code-spec-workflow get-tasks {功能名称} {任务ID} --mode complete
- 提供完成摘要
```

3. **任务执行**
   - 一次只专注于一个任务
   - 如果任务包含子任务，先从子任务开始
   - 遵循 design.md 中的实现细节
   - 根据任务中指定的需求进行验证

4. **实施指南**
   - 编写清晰、可维护的代码
   - **遵循指导文档**：遵守 tech.md 中的模式和 structure.md 中的约定
   - 遵循现有代码模式和约定
   - 包含适当的错误处理
   - 在指定位置添加单元测试
   - 为复杂逻辑添加注释

5. **验证**
   - 验证实现是否满足验收标准
   - 如存在测试则运行测试
   - 检查是否存在代码风格或类型错误
   - 确保与现有代码集成无误

6. **任务完成协议**
在使用 `/spec-execute` 完成任何任务时：
   1. **标记任务完成**：使用 get-tasks 脚本标记完成状态：
      ```bash
      # 跨平台命令：
      claude-code-spec-workflow get-tasks {功能名称} {任务ID} --mode complete
      ```
   2. **向用户确认**：明确声明“任务 X 已标记为完成”
   3. **停止执行**：不要自动进入下一个任务
   4. **等待指令**：让用户决定下一步操作

## 关键工作流规则

### 任务执行
- **仅**在实施阶段一次执行一个任务
- **关键**：停止前必须使用 get-tasks --mode complete 标记已完成任务
- **始终**在完成一个任务后停止
- **绝不**自动进入下一个任务
- **必须**等待用户请求再执行下一个任务
- **确认**任务完成状态给用户

### 需求引用
- **所有**任务必须使用 _需求：X.Y_ 格式引用具体需求
- **确保**从需求到设计再到实现的可追溯性
- **验证**实现是否符合所引用的需求

## 任务选择
如果未指定任务ID：
- 查看该spec的 tasks.md 文件
- 推荐下一个待处理任务
- 在继续前请用户确认

如果未指定功能名称：
- 检查 `.claude/specs/` 目录中的可用spec
- 若仅存在一个spec，则直接使用
- 若存在多个spec，则询问用户选择哪一个
- 若未找到任何spec，则显示错误信息

## 示例
```
/spec-execute 1 user-authentication
/spec-execute 2.1 user-authentication
```

## 重要规则
- 一次只执行一个任务
- **始终**使用 get-tasks --mode complete 标记已完成任务
- 完成任务后必须停止
- 继续前需等待用户批准
- 不得跳过任务或提前跳跃
- 向用户确认任务完成状态

## 后续步骤
任务完成后，你可以：
- 解决审查中发现的任何问题
- 如适用，运行测试
- 使用 `/spec-execute [下一个任务ID]` 执行下一个任务
- 使用 `/spec-status {功能名称}` 检查整体进度