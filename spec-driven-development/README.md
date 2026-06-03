# SD Skills - 规范驱动开发技能包

一套用于 opencode 的规范驱动开发(Specification-Driven Development)技能包，使你在 opencode 上也能具备完整的规范驱动开发能力。

## 概述

SD开发模式将开发过程分为三个清晰分离的阶段：

| 阶段 | 文档 | 核心问题 | 对应Skill |
|------|------|----------|-----------|
| 需求规格 | spec.md | 构建什么？(What) | sd-spec |
| 技术设计 | design.md | 如何构建？(How) | sd-design |
| 实现任务 | tasks.md | 执行步骤？(Steps) | sd-tasks |

**核心原则：** 规格(Spec)与设计(Design)严格分离——spec.md 只写"构建什么"，design.md 只写"如何构建"。

## Skills 列表

### 1. sd-init - 目录初始化
基于用户需求描述初始化SD目录结构，生成特性标识符和目录布局。

```
触发：用户说 "init sd"、"sd init"、"初始化规范驱动开发"
产出：.sd/specs/{feature-name}/ 目录
```

### 2. sd-spec - 规格文档管理
创建和管理 spec.md，强制"构建什么"约束，使用EARS格式编写验收条件。

```
触发：用户说 "write spec"、"写规格"、"创建规格"
前置：sd-init 已完成
产出：.sd/specs/{feature-name}/spec.md
```

### 3. sd-design - 设计文档管理
创建和管理 design.md，强制"如何构建"约束，基于spec需求生成技术方案。

```
触发：用户说 "write design"、"写设计"、"创建设计文档"
前置：sd-init 已完成（建议 spec.md 已存在）
产出：.sd/specs/{feature-name}/design.md
```

### 4. sd-tasks - 任务文档管理
基于 spec.md 和 design.md 生成逐步实现任务清单。

```
触发：用户说 "generate tasks"、"生成任务"
前置：spec.md 和 design.md 都已存在
产出：.sd/specs/{feature-name}/tasks.md
```

### 5. sd-workflow - 全流程协调
按照 sd-init → sd-spec → sd-design → sd-tasks 的顺序驱动完整流程，支持断点恢复和一致性检查。

```
触发：用户说 "sd workflow"、"sd start"、"开始SD开发"
产出：完整的 SD 文档集（spec.md + design.md + tasks.md）
```

## 目录结构

```
sd-skills/
├── sd-init/
│   └── SKILL.md          # 目录初始化技能
├── sd-spec/
│   └── SKILL.md          # 规格文档管理技能
├── sd-design/
│   └── SKILL.md          # 设计文档管理技能
├── sd-tasks/
│   └── SKILL.md          # 任务文档管理技能
├── sd-workflow/
│   └── SKILL.md          # 全流程协调技能
├── templates/
│   ├── spec_template.md  # 规格文档模板
│   ├── design_template.md # 设计文档模板
│   └── ears-format.md    # EARS格式规范
└── README.md             # 本文件
```

## 产出文件结构

完成SD流程后，项目中将生成：

```
.sd/
└── specs/
    └── {feature-name}/
        ├── spec.md      ← 需求规格（构建什么）
        ├── design.md    ← 技术设计（如何构建）
        └── tasks.md     ← 实现任务（执行步骤）
```

## 工作流程

```
用户输入需求描述
       │
       ▼
  [sd-init] 创建 .sd/specs/{feature-name}/
       │
       ▼
  [sd-spec] 生成 spec.md（6大章节：组件定位/领域术语/角色与边界/DFX约束/核心能力/数据约束）
       │
       ▼
  [sd-design] 生成 design.md（4大章节：实现模型/接口设计/数据模型）
       │
       ▼
  [sd-tasks] 生成 tasks.md（逐步实现任务清单）
       │
       ▼
  按任务顺序逐个实现代码
```

## 在 opencode 中安装使用

### 方式1：复制到 opencode skills 目录

将 `sd-skills/` 下的每个子目录复制到 opencode 的 skills 配置目录中：

```bash
# 假设 opencode skills 目录为 ~/.opencode/skills/
cp -r sd-skills/sd-init ~/.opencode/skills/
cp -r sd-skills/sd-spec ~/.opencode/skills/
cp -r sd-skills/sd-design ~/.opencode/skills/
cp -r sd-skills/sd-tasks ~/.opencode/skills/
cp -r sd-skills/sd-workflow ~/.opencode/skills/
cp -r sd-skills/templates ~/.opencode/skills/templates
```

### 方式2：在项目 .opencode 配置中引用

在项目的 opencode 配置文件中添加skills引用路径。

### 使用示例

1. **启动新特性开发：**
   > "我要实现用户登录功能，请初始化SD开发"

2. **编写规格：**
   > "请帮我写用户登录功能的规格文档"

3. **编写设计：**
   > "请基于规格文档写设计文档"

4. **生成任务：**
   > "请生成实现任务清单"

5. **一键全流程：**
   > "请用SD流程开发用户登录功能"

## 模板说明

### spec_template.md - 规格文档模板
包含6大必需章节：
1. **组件定位** - 核心职责、输入、输出、边界
2. **领域术语** - 统一语言定义
3. **角色与边界** - 角色、外部系统、交互上下文(PlantUML)
4. **DFX约束** - 性能、可靠性、安全性、可维护性、兼容性
5. **核心能力** - 业务规则、交互流程、异常场景
6. **数据约束** - 领域对象逻辑约束

### design_template.md - 设计文档模板
包含4大必需章节：
1. **实现模型** - 上下文视图、组件架构、实现设计
2. **接口设计** - 总体设计、接口清单
4. **数据模型** - 设计目标、模型实现

### ears-format.md - EARS格式规范
5种EARS模式：事件驱动、状态驱动、异常行为、可选特性、普适需求

## 与 CodeArts SDD 的差异

| 特性 | CodeArts SDD | opencode SD Skills |
|------|-------------|-------------------|
| 目录根 | `.codeartsdoer/specs/` | `.sd/specs/` |
| 触发方式 | spec-agent 自动触发 | 手动触发或指令触发 |
| 全流程协调 | 无（需手动切换skill） | sd-workflow 协调器 |
| 一致性检查 | 无 | 内置规格-设计-任务对齐检查 |
| 断点恢复 | 无 | sd-workflow 支持从断点恢复 |
| 模板文件 | 内联在SKILL.md中 | 独立templates目录 |

## 许可

本技能包基于华为云CodeArts SDD skills改编，适配opencode使用。
