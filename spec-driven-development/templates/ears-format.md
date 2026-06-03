# EARS 格式规范

## 概述
EARS（Easy Approach to Requirements Syntax）是规范驱动开发中验收条件的标准格式。

EARS模式描述需求的逻辑结构（条件 + 主体 + 响应），不依赖于特定自然语言。
所有验收条件应使用规格配置的目标语言编写。
保持EARS触发关键词和固定短语为英文（`When`、`If`、`While`、`Where`、`The system shall`、`The [system] shall`），仅将可变部分（`[event]`、`[precondition]`、`[trigger]`、`[feature is included]`、`[response/action]`）本地化为目标语言。

## 主要EARS模式

### 1. 事件驱动需求
- **模式**：When [event], the [system] shall [response/action]
- **用途**：响应特定事件或触发
- **示例**：When 用户点击结算按钮, the 结算服务 shall 验证购物车内容

### 2. 状态驱动需求
- **模式**：While [precondition], the [system] shall [response/action]
- **用途**：依赖系统状态或前置条件的行为
- **示例**：While 支付处理中, the 结算服务 shall 显示加载指示器

### 3. 异常行为需求
- **模式**：If [trigger], the [system] shall [response/action]
- **用途**：系统对错误、失败或异常情况的响应
- **示例**：If 输入无效信用卡号, the 网站 shall 显示错误提示

### 4. 可选特性需求
- **模式**：Where [feature is included], the [system] shall [response/action]
- **用途**：可选或条件特性的需求
- **示例**：Where 汽车配备天窗, the 汽车 shall 具有天窗控制面板

### 5. 普适需求
- **模式**：The [system] shall [response/action]
- **用途**：始终生效的需求和基本系统属性
- **示例**：The 手机 shall 质量小于100克

## 组合模式
- While [precondition], when [event], the [system] shall [response/action]
- When [event] and [additional condition], the [system] shall [response/action]

## 主体选择指南
- **软件项目**：使用具体系统/服务名称（如"结算服务"、"用户认证模块"）
- **流程/工作流**：使用负责团队/角色（如"支持团队"、"审核流程"）
- **非软件项目**：使用适当主体（如"营销活动"、"文档"）

## 质量标准
- 需求必须可测试、可验证，描述单一行为
- 使用客观语言："shall"表示强制行为，"should"表示建议；避免模糊术语
- 遵循EARS语法：[条件], the [系统] shall [响应/动作]
