---
name: spec-driven-development
description: 规范驱动开发技能包 - 提供完整的Spec-Driven Development开发能力。包含目录初始化、规格文档编写、设计文档生成、任务清单创建和全流程协调。核心原则：规格与设计严格分离。适用场景：(1) 新特性开发；(2) 需求分析和规格编写；(3) 技术设计；(4) 实现任务规划。触发关键词：SD开发、规范驱动、spec、design、tasks、规格文档、设计文档
---

# SD Skills - 规范驱动开发技能包

## 概述

SD开发模式是一套完整的规范驱动开发(Specification-Driven Development)能力体系，将开发过程分为三个清晰分离的阶段：

| 阶段 | 文档 | 核心问题 | 对应Skill |
|------|------|----------|-----------|
| 需求规格 | spec.md | 构建什么？(What) | sd-spec |
| 技术设计 | design.md | 如何构建？(How) | sd-design |
| 实现任务 | tasks.md | 执行步骤？(Steps) | sd-tasks |

**核心原则：** 规格(Spec)与设计(Design)严格分离——spec.md只写"构建什么"，design.md只写"如何构建"。

## 技能列表

### 1. sd-init - 目录初始化

**职责**：基于用户需求描述初始化SD目录结构，生成特性标识符和目录布局

**触发关键词**：init sd、sd init、初始化规范驱动开发

**前置条件**：无

**产出物**：`.sd/specs/{feature-name}/` 目录

### 2. sd-spec - 规格文档管理

**职责**：创建和管理spec.md，强制"构建什么"约束，使用EARS格式编写验收条件

**触发关键词**：write spec、写规格、创建规格

**前置条件**：sd-init已完成

**产出物**：`.sd/specs/{feature-name}/spec.md`

**文档结构**：
- 组件定位（核心职责、输入、输出、边界）
- 领域术语（统一语言定义）
- 角色与边界（角色、外部系统、交互上下文）
- DFX约束（性能、可靠性、安全性、可维护性、兼容性）
- 核心能力（业务规则、交互流程、异常场景）
- 数据约束（领域对象逻辑约束）

### 3. sd-design - 设计文档管理

**职责**：创建和管理design.md，强制"如何构建"约束，基于spec需求生成技术方案

**触发关键词**：write design、写设计、创建设计文档

**前置条件**：sd-init已完成（建议spec.md已存在）

**产出物**：`.sd/specs/{feature-name}/design.md`

**文档结构**：
- 实现模型（上下文视图、组件架构、实现设计）
- 接口设计（总体设计、接口清单）
- 数据模型（设计目标、模型实现）

### 4. sd-tasks - 任务文档管理

**职责**：基于spec.md和design.md生成逐步实现任务清单

**触发关键词**：generate tasks、生成任务

**前置条件**：spec.md和design.md都已存在

**产出物**：`.sd/specs/{feature-name}/tasks.md`

### 5. sd-workflow - 全流程协调

**职责**：按照sd-init → sd-spec → sd-design → sd-tasks的顺序驱动完整流程，支持断点恢复和一致性检查

**触发关键词**：sd workflow、sd start、开始SD开发

**产出物**：完整的SD文档集（spec.md + design.md + tasks.md）

**核心能力**：
- 自动流程编排
- 断点恢复
- 规格与设计一致性检查
- 进度跟踪

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
└── SKILL.md              # 本文件
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
  [sd-spec] 生成 spec.md
       │     - 组件定位
       │     - 领域术语
       │     - 角色与边界
       │     - DFX约束
       │     - 核心能力
       │     - 数据约束
       │
       ▼
  [sd-design] 生成 design.md
       │       - 实现模型
       │       - 接口设计
       │       - 数据模型
       │
       ▼
  [sd-tasks] 生成 tasks.md
       │       - 任务分解
       │       - 依赖关系
       │       - 实施步骤
       │
       ▼
  按任务顺序逐个实现代码
```

## 安装部署

### 方式一：项目级安装（推荐）

**步骤**：

1. 复制技能包到项目目录：
   ```
   你的项目/.opencode/skills/sd-spec-driven-development/
   └── sd-skills/ (包含所有子技能)
   ```

2. 配置项目设置：
   在 `opencode.json` 中添加：
   ```json
   {
     "skill": {
       "sd-spec-driven-development": {
         "enabled": true,
         "auto_trigger": false
       }
     }
   }
   ```

### 方式二：全局安装

**步骤**：

1. 复制到全局配置目录：
   ```
   Windows: %USERPROFILE%\.config\opencode\skills\sd-spec-driven-development\
   Linux/macOS: ~/.config/opencode/skills/sd-spec-driven-development/
   ```

2. 复制templates目录：
   ```
   Windows: %USERPROFILE%\.config\opencode\skills\templates\
   Linux/macOS: ~/.config/opencode/skills/templates/
   ```

## 使用示例

### 场景1：新特性开发

```
用户：我要实现用户登录功能，请初始化SD开发

AI：[触发sd-workflow]
正在启动SD开发流程...

步骤1：目录初始化
✓ 创建 .sd/specs/user-login/

步骤2：规格文档编写
✓ 生成 spec.md
  - 组件定位：用户认证组件
  - 核心能力：登录、登出、会话管理
  - DFX约束：响应时间<200ms，可用性99.9%

步骤3：设计文档编写
✓ 生成 design.md
  - 实现模型：JWT + Redis会话
  - 接口设计：POST /api/auth/login
  - 数据模型：User, Session

步骤4：任务清单生成
✓ 生成 tasks.md
  - 任务1：实现User模型
  - 任务2：实现JWT工具类
  - 任务3：实现登录接口
  - 任务4：编写单元测试

SD开发流程完成，可以开始实现任务。
```

### 场景2：仅编写规格文档

```
用户：请帮我写用户注册功能的规格文档

AI：[触发sd-spec]
正在编写规格文档...

检查前置条件：
✓ sd-init已完成

生成spec.md：
✓ 组件定位：用户注册组件
✓ 领域术语：注册、验证、激活
✓ 角色与边界：用户、邮件系统、短信系统
✓ DFX约束：并发注册支持、防刷机制
✓ 核心能力：邮箱注册、手机号注册、验证码
✓ 数据约束：邮箱格式、密码强度

规格文档已完成：.sd/specs/user-register/spec.md
```

### 场景3：断点恢复

```
用户：继续之前的SD开发

AI：[触发sd-workflow]
检查SD开发进度...

当前进度：
✓ sd-init - 已完成
✓ sd-spec - 已完成（spec.md存在）
✗ sd-design - 未完成（design.md不存在）
✗ sd-tasks - 未完成

从断点恢复，继续执行：
→ [sd-design] 生成 design.md
```

## 模板说明

### spec_template.md - 规格文档模板

包含6大必需章节：

1. **组件定位**
   - 核心职责
   - 输入
   - 输出
   - 边界

2. **领域术语**
   - 统一语言定义
   - 业务概念说明

3. **角色与边界**
   - 角色
   - 外部系统
   - 交互上下文（PlantUML）

4. **DFX约束**
   - 性能要求
   - 可靠性要求
   - 安全性要求
   - 可维护性要求
   - 兼容性要求

5. **核心能力**
   - 业务规则
   - 交互流程
   - 异常场景

6. **数据约束**
   - 领域对象逻辑约束

### design_template.md - 设计文档模板

包含4大必需章节：

1. **实现模型**
   - 上下文视图
   - 组件架构
   - 实现设计

2. **接口设计**
   - 总体设计
   - 接口清单

3. **数据模型**
   - 设计目标
   - 模型实现

### ears-format.md - EARS格式规范

5种EARS模式：
- 事件驱动
- 状态驱动
- 异常行为
- 可选特性
- 普适需求

## 核心优势

### 1. 规格与设计分离
- spec.md只关注"构建什么"
- design.md只关注"如何构建"
- 避免需求和技术实现混淆

### 2. 标准化文档结构
- 6大规格章节
- 4大设计章节
- 确保文档完整性

### 3. 一致性保证
- 设计必须基于规格
- 任务必须对应设计
- 全链路可追溯

### 4. 断点恢复
- 自动检测已完成阶段
- 从断点继续执行
- 无需重复工作

## 最佳实践

### 1. 新特性开发
使用sd-workflow一键完成全流程

### 2. 规格先行
先完成spec.md，充分理解需求后再设计

### 3. 设计对齐
确保design.md完全覆盖spec.md的需求

### 4. 任务细化
tasks.md的任务要具体、可执行、可验证

### 5. 增量开发
大特性拆分为多个小特性，逐个使用SD流程

## 故障排查

### 问题1：sd-init失败
检查是否有权限创建.sd目录

### 问题2：spec.md无法生成
确认sd-init已完成，检查需求描述是否清晰

### 问题3：design.md与spec不一致
使用sd-workflow的一致性检查功能

### 问题4：任务无法执行
检查tasks.md是否基于最新的design.md生成

## 版本信息

- **版本**: 1.0.0
- **发布日期**: 2026-05-29
- **改编来源**: 华为云CodeArts SDD skills

---

**维护者**: AI Assistant  
**最后更新**: 2026-05-29
