# Ralph - 自主代理框架

**中文版** | [English](README.md)

一个智能自主代理框架，能将复杂项目分解成可管理的用户故事并逐步执行。Ralph 设计用于与拥有各种技能和工具的命令行 AI 系统配合工作。

## 🎯 快速概览

Ralph 能让 AI 系统：

1. **分析**你的项目结构和可用资源
2. **生成**智能的项目需求文档（PRD）
3. **呈现**计划供你确认
4. **自动执行**所有任务（人类监督）

```
用户请求 → AI分析 → PRD生成 → 用户确认 → Ralph执行
```

## ✨ 核心特性

### 🤖 AI 驱动的 PRD 生成
无需手动写 PRD。你的 AI 系统：
- 扫描项目结构
- 识别可用技能
- 自动生成智能 PRD
- 展示给你审核批准

### 📋 上下文感知执行
- **contextMap**：将资源映射到每个用户故事
- **requiredSkills**：声明需要的能力
- **userStories**：将工作分解为原子性的可执行单位

### ⏸️ 暂停和恢复控制
- 随时暂停执行
- 任何时刻审查进度
- 通过更正或新指导恢复
- 完整的会话持久化

### 🔍 逐轮执行
- 每次迭代在全新上下文中运行
- 每轮后保存检查点
- 进度日志和维护
- 敏感操作标记待审批

### 🌳 多任务类型支持
Ralph 能处理不同的项目类型：
- **code**：软件开发和代码重构
- **content**：文档、论文、博客、指南
- **research**：数据分析和研究项目
- **data**：数据处理和分析
- **devops**：基础设施和部署
- **testing**：测试套件创建和验证
- **orchestrator**：复杂多步骤工作流

## 🚀 快速开始

### 基本用法

```bash
# 创建并启动会话
ralph.mjs create --prd path/to/prd.json --start

# 实时查看日志
ralph.mjs logs <session-id> --follow

# 暂停执行
ralph.mjs pause <session-id> --reason "等待审查"

# 恢复执行并提供指导
ralph.mjs resume <session-id> --guidance "改用这个方法"

# 查看会话状态
ralph.mjs status <session-id>
```

### 完整 CLI 参考

```bash
ralph.mjs --help
```

## 📚 文档

### 面向 AI 系统
- **[SKILL.md](SKILL.md)** - Ralph 的功能和使用方法
- **[docs/AI_WORKFLOW.md](docs/AI_WORKFLOW.md)** - AI 系统的 13 阶段工作流
- **[docs/PRD_GENERATOR.md](docs/PRD_GENERATOR.md)** - 如何生成智能 PRD

### 示例
- **[examples/MCM_PAPER_GUIDE.md](examples/MCM_PAPER_GUIDE.md)** - 完整论文写作示例
- **[examples/mcm-paper-prd.json](examples/mcm-paper-prd.json)** - 示例 PRD 结构

### 任务特定指南
- **[prompts/base.md](prompts/base.md)** - 所有任务的基础指令
- **[prompts/content.md](prompts/content.md)** - 内容/写作 PRD
- **[prompts/code.md](prompts/code.md)** - 代码开发 PRD
- **[prompts/research.md](prompts/research.md)** - 研究项目
- **[prompts/data.md](prompts/data.md)** - 数据分析
- **[prompts/devops.md](prompts/devops.md)** - 基础设施任务
- **[prompts/testing.md](prompts/testing.md)** - 测试 PRD
- **[prompts/orchestrator.md](prompts/orchestrator.md)** - 复杂工作流

## 🏗️ 架构

Ralph 包含以下组件：

### CLI 层
**ralph.mjs** - 用于创建和管理会话的命令行界面

### 守护进程层
- **daemon/server.mjs** - HTTP API 服务器
- **daemon/session-manager.mjs** - 会话生命周期管理
- **daemon/turn-engine.mjs** - 受控逐轮执行引擎
- **daemon/storage.mjs** - SQLite 持久化层
- **daemon/ui.html** - 可选的监控 Web UI

### 提示模板
- **prompts/base.md** - Ralph 的通用指令
- **prompts/{taskType}.md** - 任务特定的指导

## 📖 PRD 结构

典型的 PRD 如下所示：

```json
{
  "description": "写我的研究论文",
  "taskType": "content",
  "requiredSkills": [
    "支持数学符号的文档格式化",
    "图表渲染和验证",
    "参考文献管理"
  ],
  "contextMap": {
    "US001": {
      "references": ["docs/problem_statement.md"],
      "code_files": ["src/experiment.py"],
      "experiments": ["results/exp1_output.json"]
    }
  },
  "userStories": [
    {
      "id": "US001",
      "title": "写引言",
      "acceptanceCriteria": [
        "阅读问题陈述",
        "写 300-500 字",
        "包含问题概览和动机"
      ],
      "priority": 1,
      "passes": false
    }
  ]
}
```

## 🔄 工作流

### 第 1-8 阶段：AI 准备
AI 系统分析你的项目并生成智能 PRD

### 第 9 阶段：用户确认 ⭐
AI 展示计划给你：
```
结构：
- 6 个部分要写（引言、文献综述、方法、结果、讨论、结论）

要读的资源：
- 代码：src/model.py, src/experiment.py
- 数据：results/output.json, results/plots.png
- 参考：refs/methodology.bib

需要的技能：
✓ QMD 格式化（使用 Quarto Authoring）
✓ 图表渲染（使用 Quarto）
✓ 参考文献管理（使用 Citation Manager）

确认？(yes/no/adjust)
```

你批准或请求更改。**没有你的许可，不会自动化。**

### 第 10-13 阶段：Ralph 执行
Ralph 运行 PRD，监控进度并处理错误

## 💡 为什么选择 Ralph？

### ✅ 智能自动化
你的 AI 理解实际项目结构并生成定制化的计划

### ✅ 人类监督
你在自动化开始前审查和批准计划

### ✅ 优雅的处理
完整的暂停/恢复能力、进度持久化和错误处理

### ✅ 上下文感知
contextMap 确保 Ralph 拥有每项任务所需的所有上下文

### ✅ 灵活可扩展
支持自定义任务类型、技能和工作流

## 📦 项目结构

```
ralph/
├── ralph.mjs                 # CLI 入口点
├── SKILL.md                  # 技能文档
├── README.md                 # 英文 README
├── README.zh.md              # 中文 README
├── daemon/
│   ├── server.mjs           # HTTP 守护进程
│   ├── session-manager.mjs  # 会话管理
│   ├── turn-engine.mjs      # 执行引擎
│   ├── storage.mjs          # 数据持久化
│   └── ui.html              # Web UI
├── prompts/
│   ├── base.md              # 基础指令
│   ├── content.md           # 内容 PRD
│   ├── code.md              # 代码 PRD
│   ├── research.md          # 研究 PRD
│   ├── data.md              # 数据 PRD
│   ├── devops.md            # DevOps PRD
│   ├── testing.md           # 测试 PRD
│   └── orchestrator.md      # 复杂工作流
├── docs/
│   ├── AI_WORKFLOW.md       # 13 阶段工作流指南
│   ├── PRD_GENERATOR.md     # PRD 生成指南
│   └── [其他指南]
└── examples/
    ├── mcm-paper-prd.json   # 示例 PRD
    └── MCM_PAPER_GUIDE.md   # 使用示例
```

## 🔗 集成

Ralph 无缝配合以下工具：
- **Claude Agent SDK** - 逐轮执行
- **命令行 AI 系统** - Claude、其他 AI 模型
- **自定义技能** - 用你自己的工具扩展
- **版本控制** - 代码 PRD 的 Git 集成
- **文件系统** - 任何项目结构

## 📝 示例：写论文

```bash
# 用户："Use Ralph to write my research paper"
# ↓
# AI 分析：src/、data/、refs/ 文件夹
# ↓
# AI 检查：有 Quarto Authoring、Quarto Rendering 技能
# ↓
# AI 生成 PRD：
#   - 6 个用户故事（各部分）
#   - contextMap 指向代码、数据、参考
#   - requiredSkills：["QMD 格式化", "图表渲染", ...]
# ↓
# AI 展示 PRD 给用户
# ↓
# 用户："看起来不错！"
# ↓
ralph.mjs create --prd generated_prd.json --start
# ↓
# Ralph 执行所有故事
# ↓
# 你得到一篇完整、精细的研究论文！
```

## 🛠️ 命令

### 会话管理

```bash
# 创建新会话
ralph.mjs create --prd <prd-file> [--start]

# 列出所有会话
ralph.mjs list

# 获取会话状态
ralph.mjs status <session-id>

# 启动会话
ralph.mjs start <session-id>

# 暂停会话
ralph.mjs pause <session-id> --reason "..."

# 恢复会话
ralph.mjs resume <session-id> --guidance "..."

# 在执行期间注入指导
ralph.mjs inject <session-id> --message "..."

# 中止会话
ralph.mjs abort <session-id>

# 销毁会话（完全删除）
ralph.mjs destroy <session-id>
```

### 监控

```bash
# 查看会话日志
ralph.mjs logs <session-id>

# 实时跟踪日志
ralph.mjs logs <session-id> --follow

# 显示会话树（父子关系）
ralph.mjs tree <session-id>

# 列出子会话
ralph.mjs children <session-id>
```

## 🤝 贡献

Ralph 设计用于扩展。你可以：

- 创建自定义任务类型（添加新的 `prompts/{type}.md`）
- 开发新技能（与你的 AI 系统集成）
- 扩展转向引擎（添加新的命令类型）
- 自定义存储层

## 📄 许可

MIT

## 🤔 常见问题

**Q：我需要手动写 PRD 吗？**
A：不需要！你的 AI 系统会自动生成。你只需审查和确认。

**Q：我能暂停执行吗？**
A：可以，随时都行。Ralph 保存所有进度，可以通过更正恢复。

**Q：如果 Ralph 犯错了呢？**
A：用 `ralph.mjs inject` 注入指导，Ralph 在下一轮调整。

**Q：Ralph 能处理复杂项目吗？**
A：可以！使用 "orchestrator" 任务类型或启用敏感工具审批。

**Q：contextMap 是什么？**
A：一个将用户故事 ID 映射到 Ralph 需要为该故事读取的文件的映射。它确保 Ralph 拥有所有上下文。

**Q：我能用自己的 AI 系统使用 Ralph 吗？**
A：可以！Ralph 使用 Claude Agent SDK，可以为其他模型适配。

---

**准备开始了吗？** 查看 [SKILL.md](SKILL.md) 或 [docs/AI_WORKFLOW.md](docs/AI_WORKFLOW.md)。
