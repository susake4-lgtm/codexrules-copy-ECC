# codexrules-copy-ECC

这是一个面向 Codex 的全局规则仓库。

它只保留真正会被 Codex 运行时读取的内容，不包含：

1. `docs/` 里的规划、结论、试运行记录
2. `everything-claude-code/` 参考仓库
3. 本机私有日志、认证、backup、trusted project 路径

## 项目思路

这个仓库的核心思路不是“再造一套上层方法论”，而是把已经验证过的协作规则，压到 Codex 真正能承载的全局层里。

分层如下：

1. `.codex/AGENTS.md`
   - 放机器级默认协作规则
   - 只写跨项目稳定的默认行为
   - `plan` 确认后提醒判断是否需要 skills / MCP
2. `.codex/config.toml`
   - 放运行时配置
   - 只保留适合公开复用的基线，不带本机私有 `projects.*`
3. `.codex/agents/*`
   - 放角色化只读 agent
   - 当前先保留 `explorer`、`reviewer`、`docs-researcher`
4. `.agents/skills/*`
   - 放高复用、强流程、明确触发条件的全局 skills

也就是说，这个仓库承接的是“运行时层”和“高复用执行层”，而不是规划讨论层。

## 设计原则

1. `global-first`
   - 先收本机级默认规则
   - 项目级 `AGENTS.md` 只在仓库存在特殊边界时再补
2. `runtime-only`
   - 只放运行时会读到的内容，不把长篇设计文档混进来
3. `layered`
   - 总规则、运行配置、角色提示词、skills 明确分层
   - 全局规则是主层，skills / MCP 是默认能力层，项目级规则是差异层
4. `safe rollout`
   - 推荐启用顺序是：
   - `~/.codex/AGENTS.md`
   - `~/.codex/agents/*`
   - `~/.codex/config.toml`
   - `~/.agents/skills`
5. `portable`
   - 仓库里不写你的本机私有 trusted project 路径
   - 不把 logs、auth、backups 一起公开

## 目录结构

```text
.codex/
├── AGENTS.md
├── config.toml
└── agents/
    ├── explorer.toml
    ├── reviewer.toml
    └── docs-researcher.toml

.agents/
└── skills/
    ├── code-review-standard/
    ├── find-skills/
    ├── security-review-standard/
    ├── session-save-handoff/
    ├── skill-create/
    └── verification-loop/
```

## 当前包含的全局 skills

1. `verification-loop`
2. `code-review-standard`
3. `security-review-standard`
4. `session-save-handoff`
5. `skill-create`
6. `find-skills`

## 当前默认运行口径

1. `plan` 确认后再进入实施。
2. `plan` 确认后，会先提醒判断现有 skills / MCP 是否已经足够，或是否值得补充新的能力层。
3. 这个提醒不等于自动新增 skills / MCP。
4. 如果项目没有明显仓库特化边界，可以只用全局规则、全局 skills 和按需启用的 MCP，不必再写项目级 `AGENTS.md`。

## 安装建议

### 1. AGENTS

```bash
cp .codex/AGENTS.md ~/.codex/AGENTS.md
```

### 2. agents

```bash
mkdir -p ~/.codex/agents
cp .codex/agents/*.toml ~/.codex/agents/
```

### 3. config

`config.toml` 建议合并，不建议直接覆盖你已有的本机配置，尤其是：

1. `projects.*`
2. 本机特有的 `model`
3. 你已经在用的其他 runtime 选项

### 4. skills

推荐把仓库里的 `.agents/skills` 暴露到：

```bash
mkdir -p ~/.agents
ln -snf "$(pwd)/.agents/skills" ~/.agents/skills
```

## 备注

1. 这个仓库是“可公开复用的运行时配置版本”，不是完整设计档归档。
2. 如果你要看为什么这样分层、为什么这样 rollout，需要回到原项目里的 `docs/`。
3. 如果你要继续扩展第二批 skills，建议保持同样的分层纪律，不要把项目级规则重新抬到全局层。
