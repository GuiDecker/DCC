# 智能体编排

## 可用智能体

ECC 智能体随 `ecc@ecc` 插件一起分发，不在 `~/.claude/agents/` 目录中。
它们通过 Agent 工具以插件作用域的 `subagent_type` 调用：

```text
Agent(subagent_type: "dcc:planner", prompt: "...")
```

| 代理 | 用途 | 使用时机 |
|-------|---------|-------------|
| dcc:planner | 实现规划 | 复杂功能、重构 |
| dcc:architect | 系统设计 | 架构决策 |
| dcc:tdd-guide | 测试驱动开发 | 新功能、错误修复 |
| dcc:code-reviewer | 代码审查 | 编写代码后 |
| dcc:security-reviewer | 安全分析 | 提交前 |
| dcc:build-error-resolver | 修复构建错误 | 构建失败时 |
| dcc:e2e-runner | 端到端测试 | 关键用户流程 |
| dcc:refactor-cleaner | 清理死代码 | 代码维护 |
| dcc:doc-updater | 文档 | 更新文档 |
| dcc:rust-reviewer | Rust 代码审查 | Rust 项目 |

完整 68 个智能体的清单参见 `/ecc:ecc-guide`。

## 即时智能体使用

无需用户提示：

1. 复杂的功能请求 - 使用 **dcc:planner** 智能体
2. 刚编写/修改的代码 - 使用 **dcc:code-reviewer** 智能体
3. 错误修复或新功能 - 使用 **dcc:tdd-guide** 智能体
4. 架构决策 - 使用 **dcc:architect** 智能体

## 并行任务执行

对于独立操作，**始终**使用并行任务执行：

```markdown
# 良好：并行执行
同时启动 3 个智能体：
1. 智能体 1：认证模块的安全分析
2. 智能体 2：缓存系统的性能审查
3. 智能体 3：工具类的类型检查

# 不良：不必要的顺序执行
先智能体 1，然后智能体 2，最后智能体 3

```

## 多视角分析

对于复杂问题，使用拆分角色的子智能体：

* 事实审查员
* 高级工程师
* 安全专家
* 一致性审查员
* 冗余检查器
