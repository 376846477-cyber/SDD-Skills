---
name: harness-dev-flow
description: Harness工程开发模式Skill - 端到端的软件工程开发流程管理。涵盖设计、编码、测试、质量、部署全生命周期。适用场景：(1) 新项目启动；(2) 功能开发；(3) 代码重构；(4) 质量提升。触发关键词：harness开发模式、开发流程、工程化、设计文档、代码开发、测试流程、质量检查、部署流程
---

# Harness工程开发模式

## 概述

Harness工程开发模式是一套完整的软件工程开发流程管理体系，覆盖从需求分析到生产部署的全生命周期。通过集成最佳实践和自动化工具，帮助开发团队提升代码质量和开发效率。

## 核心理念

### 1. 全生命周期管理
```
需求分析 → 技术设计 → 代码实现 → 单元测试 → 质量检查 → 集成测试 → 部署发布
```

### 2. 质量左移
- 在开发早期发现和修复问题
- 自动化测试和质量门禁
- 持续集成和持续交付

### 3. 可追溯性
- 需求→设计→代码→测试的全链路追溯
- 完整的变更历史和审计日志

## 开发流程阶段

### 阶段1：需求与设计 (harness-design)

**触发关键词**：设计文档、技术设计、架构设计、写设计

**主要活动**：
- 需求分析与验收条件定义
- 技术架构设计
- 数据模型设计
- 接口设计
- 文档产出（设计文档.md）

**输出产物**：
- 技术设计文档
- 架构图
- 数据模型图
- API接口定义

### 阶段2：编码实现 (harness-coding)

**触发关键词**：开始编码、实现功能、写代码

**主要活动**：
- 代码框架搭建
- 核心功能实现
- 单元测试编写
- 代码评审
- 设计一致性验证

**输出产物**：
- 源代码文件
- 单元测试文件
- 代码评审记录
- 代码-设计一致性报告

### 阶段2.5：代码-设计一致性验证 (code-design-verify)

**触发关键词**：设计一致性、代码验证、一致性检查

**主要活动**：
- 功能一致性检查
- 代码与设计对应检查
- 代码真实存在性检查
- 设计功能到代码行号映射
- 一致性报告生成

**输出产物**：
- 代码-设计一致性检查报告
- 功能映射清单
- 问题修复建议

### 阶段3：测试验证 (harness-testing)

**触发关键词**：运行测试、测试报告、测试流程

**主要活动**：
- 单元测试执行
- 集成测试执行
- 测试覆盖率分析
- 测试报告生成

**输出产物**：
- 测试报告
- 覆盖率报告
- 测试失败分析

### 阶段4：质量保证 (harness-quality)

**触发关键词**：质量检查、代码质量、质量门禁

**主要活动**：
- 代码规范检查
- 静态分析
- 安全漏洞扫描
- 性能分析
- 质量门禁验证

**输出产物**：
- 质量报告
- 问题清单
- 改进建议

### 阶段5：构建部署 (harness-deploy)

**触发关键词**：构建、部署、发布

**主要活动**：
- 构建流水线执行
- 环境部署
- 集成测试验证
- 生产发布

**输出产物**：
- 构建产物
- 部署记录
- 发布说明

## 快速开始

### 场景1：新功能开发

```
用户：我要开发一个用户认证功能

AI：[触发harness-dev-flow]
已启动Harness工程开发模式，开始用户认证功能开发流程：

📋 阶段1：需求与设计
1. 需求分析：用户认证功能需求
2. 技术设计：认证架构设计
3. 接口设计：认证API定义

[自动调用harness-design skill]
...
```

### 场景2：代码质量提升

```
用户：检查当前代码质量

AI：[触发harness-quality]
正在执行质量检查流程：

✓ 代码规范检查
✓ 静态分析
✓ 安全扫描
✓ 测试覆盖率分析

质量报告已生成：
- 代码评分: 85/100
- 发现问题: 12个
- 改进建议: 8条
```

### 场景3：完整开发流程

```
用户：使用Harness开发模式开发订单管理模块

AI：[触发harness-dev-flow]
已启动完整的Harness开发流程：

阶段1：需求与设计 [进行中]
├─ 需求分析
├─ 技术设计
└─ 设计文档生成

阶段2：编码实现 [待开始]
阶段2.5：设计一致性验证 [待开始]
阶段3：测试验证 [待开始]
阶段4：质量保证 [待开始]
阶段5：构建部署 [待开始]

当前：正在执行设计阶段...
```

### 场景4：编码完成自动验证设计一致性

```
用户：编码阶段已完成

AI：编码阶段完成，自动触发设计一致性验证...

━━━━━━━━━━━━━━━━━━━━━

📋 设计一致性验证

步骤1：文档解析
├─ 读取设计文档：docs/design/order-design.md
├─ 提取功能模块：5个
└─ 提取接口定义：12个

步骤2：代码扫描
├─ 扫描目录：src/order/
├─ 发现文件：8个
└─ 代码行数：1250行

步骤3：功能一致性检查
┌──────────────┬──────────────────┬──────┐
│ 设计功能      │ 代码实现          │ 状态 │
├──────────────┼──────────────────┼──────┤
│ 创建订单      │ src/order/service.py:45│✓│
│ 取消订单      │ src/order/service.py:89│✓│
│ 订单查询      │ src/order/service.py:132│✓│
│ 订单列表      │ src/order/service.py:178│✓│
│ 订单统计      │ src/order/service.py:215│✓│
└──────────────┴──────────────────┴──────┘
一致率：5/5 (100%)

步骤4：接口对应检查
设计接口 → 代码位置映射：
- POST /api/orders → src/order/routes.py:18
- GET /api/orders/{id} → src/order/routes.py:35
- PUT /api/orders/{id}/cancel → src/order/routes.py:52
- GET /api/orders → src/order/routes.py:68
- GET /api/orders/stats → src/order/routes.py:95
一致率：12/12 (100%)

步骤5：代码真实存在性检查
✓ 所有文件存在
✓ 所有函数已实现
✓ 无空实现/TODO

━━━━━━━━━━━━━━━━━━━━━

📊 一致性验证结果

综合评分：100/100
评级：✓ 通过

验证结论：
- 功能完整性：100%
- 代码与设计一致性：100%
- 代码真实存在性：100%

详细报告：reports/code-design-consistency-report.md

━━━━━━━━━━━━━━━━━━━━━

✅ 设计一致性验证通过

自动进入下一阶段：测试验证

阶段3：测试验证 [进行中]
├─ 运行单元测试
├─ 执行集成测试
└─ 生成测试报告
```

## 工作流程

### 标准开发流程

```
1. 需求输入
   ├─ 用户描述需求
   └─ AI分析需求类型

2. 自动阶段识别
   ├─ 新功能 → 完整流程（阶段1-5）
   ├─ 设计 → 阶段1
   ├─ 编码 → 阶段2
   ├─ 测试 → 阶段3
   ├─ 质量 → 阶段4
   └─ 部署 → 阶段5

3. 子Skill调用
   └─ 调用对应阶段的子skill

4. 阶段执行
   ├─ 执行该阶段任务
   ├─ 生成阶段产物
   └─ 验证阶段完成

5. 设计一致性验证（编码后自动触发）
   ├─ 解析设计文档和代码
   ├─ 验证功能一致性
   ├─ 检查代码与设计对应
   ├─ 确认代码真实存在
   └─ 生成一致性报告

6. 阶段流转
   ├─ 当前阶段完成
   ├─ 一致性验证通过
   ├─ 触发下一阶段
   └─ 或等待用户确认

7. 完成确认
   └─ 所有阶段完成，生成完整报告
```

### 决策逻辑

```python
def determine_workflow(user_input):
    """根据用户输入确定工作流程"""
    
    keywords = {
        '设计': 'harness-design',
        '架构': 'harness-design',
        '编码': 'harness-coding',
        '实现': 'harness-coding',
        '测试': 'harness-testing',
        '质量': 'harness-quality',
        '部署': 'harness-deploy',
    }
    
    for keyword, skill_name in keywords.items():
        if keyword in user_input:
            return skill_name
    
    # 默认完整流程
    return 'full_workflow'
```

## 目录结构

项目采用以下标准目录结构：

```
project/
├── .harness/              # Harness配置目录
│   ├── config.yaml        # 开发流程配置
│   ├── design/            # 设计文档
│   ├── reports/           # 各阶段报告
│   └── templates/         # 文档模板
├── docs/                  # 项目文档
│   ├── design/            # 设计文档
│   └── api/               # API文档
├── src/                   # 源代码
│   ├── main/              # 主代码
│   └── test/              # 测试代码
├── test/                  # 测试相关
│   ├── unit/              # 单元测试
│   ├── integration/       # 集成测试
│   └── reports/           # 测试报告
└── reports/               # 项目报告
    ├── quality/           # 质量报告
    └── deployment/        # 部署报告
```

## 配置文件

### .harness/config.yaml

```yaml
harness:
  project_name: 项目名称
  version: 1.0.0
  
  # 开发流程配置
  workflow:
    auto_proceed: true      # 自动进入下一阶段
    quality_gate: true      # 启用质量门禁
    require_review: true    # 需要代码评审
    design_consistency_check: true  # 启用设计一致性验证
  
  # 设计一致性验证配置
  design_consistency:
    enabled: true
    threshold: 90           # 一致率阈值(%)
    block_on_failure: true  # 验证失败是否阻断流程
    report_format: markdown # 报告格式
    
  # 质量标准
  quality:
    code_coverage: 80       # 代码覆盖率阈值
    test_pass_rate: 95      # 测试通过率阈值
    complexity_limit: 10    # 代码复杂度限制
    security_level: high    # 安全扫描级别
    design_consistency: 90  # 设计一致性阈值
    
  # 阶段配置
  stages:
    design:
      enabled: true
      templates:
        - architecture.md
        - api-design.md
        - data-model.md
        
    coding:
      enabled: true
      standards: clean-code
      review_required: true
      design_consistency_check: true  # 编码后验证
        
    testing:
      enabled: true
      coverage_threshold: 80
      parallel: true
        
    quality:
      enabled: true
      tools:
        - sonarqube
        - checkstyle
        - security-scan
        
    deploy:
      enabled: true
      environments:
        - dev
        - staging
        - prod
```

## 最佳实践

### 1. 需求驱动开发

```
用户：开发一个用户注册功能，需要邮箱验证

AI：已识别需求，开始设计阶段：

📋 需求分析
- 功能：用户注册
- 验证方式：邮箱验证
- 安全要求：密码加密

✏️ 技术设计
- 架构：MVC模式
- 数据库：用户表设计
- API：注册接口设计

📄 生成设计文档...
```

### 2. 测试驱动开发

```
用户：实现登录功能，先写测试

AI：采用TDD开发模式：

🔴 红灯：编写失败的测试
├─ test_login_success()
├─ test_login_invalid_password()
└─ test_login_user_not_found()

🟢 绿灯：实现最小代码
└─ 实现login()方法

🔄 重构：优化代码质量
└─ 提取公共逻辑

测试覆盖率：95%
```

### 3. 持续集成

```
用户：提交代码，自动运行测试

AI：触发CI流程：

1. 代码检查 ✓
   - 代码规范: 通过
   - 静态分析: 通过

2. 单元测试 ✓
   - 测试数: 45
   - 通过: 45
   - 覆盖率: 87%

3. 质量门禁 ✓
   - 所有指标达标

可以合并到主分支！
```

## 质量标准

### 代码质量指标

| 指标 | 标准值 | 说明 |
|------|--------|------|
| 代码覆盖率 | ≥ 80% | 单元测试覆盖率 |
| 测试通过率 | ≥ 95% | 所有测试通过率 |
| 代码复杂度 | ≤ 10 | 单个函数圈复杂度 |
| 重复代码率 | ≤ 5% | 代码重复率 |
| 安全漏洞 | 0 | 高危安全漏洞数 |
| 设计一致性 | ≥ 90% | 代码与设计一致率 |

### 质量门禁规则

```yaml
quality_gates:
  - name: 代码覆盖率
    metric: code_coverage
    threshold: 80
    operator: ">="
    
  - name: 测试通过率
    metric: test_pass_rate
    threshold: 95
    operator: ">="
    
  - name: 安全漏洞
    metric: security_vulnerabilities
    threshold: 0
    operator: "=="
    
  - name: 代码复杂度
    metric: cyclomatic_complexity
    threshold: 10
    operator: "<="
    
  - name: 设计一致性
    metric: design_consistency
    threshold: 90
    operator: ">="
    description: "代码实现与设计文档的一致性"
```

## 故障排查

### 问题1：质量门禁不通过

**现象**：代码覆盖率低于80%

**解决方案**：
```
用户：质量门禁不通过怎么办？

AI：分析质量报告：

❌ 不通过项目：
- 代码覆盖率: 75% < 80%

📊 未覆盖代码：
- src/auth.py: login() 函数
- src/user.py: update_profile() 函数

💡 建议：
1. 为login()添加测试用例
2. 为update_profile()添加测试用例

预估覆盖率提升：75% → 85%
```

### 问题2：测试失败

**现象**：多个测试用例失败

**解决方案**：
```
用户：测试失败了

AI：测试失败分析：

❌ 失败测试：3个
1. test_login_invalid_password
   原因：密码验证逻辑错误
   位置：src/auth.py:45

2. test_user_registration
   原因：数据库连接超时
   位置：src/db.py:120

💡 修复建议：
1. 修正密码验证条件
2. 增加数据库连接重试机制
```

### 问题3：设计一致性验证失败

**现象**：代码与设计文档一致性低于90%

**解决方案**：
```
用户：设计一致性验证失败了

AI：设计一致性分析：

❌ 一致率：78% < 90%

📊 不一致详情：

1. 功能缺失：
   - 设计功能：邮件验证
   - 状态：未实现
   - 建议：在src/auth.py中添加邮件验证逻辑

2. 接口不匹配：
   - 设计接口：GET /api/users/{id}/profile
   - 代码实现：GET /api/users/{id}
   - 位置：src/routes/user.py:42
   - 建议：修改接口路径或更新设计文档

3. 数据模型差异：
   - 设计字段：user.status
   - 代码实现：缺失
   - 位置：src/models/user.py
   - 建议：添加status字段或更新设计文档

4. 空实现：
   - 文件：src/payment/service.py:89
   - 函数：process_refund()
   - 状态：只有TODO注释
   - 建议：实现退款逻辑

💡 修复方案：

方案A：补全缺失功能
预估一致率：78% → 95%

方案B：更新设计文档
预估一致率：78% → 100%

请选择修复方案：
```

### 问题4：代码功能无法与设计对应

**现象**：设计文档中的功能在代码中找不到对应实现

**解决方案**：
```
用户：某个功能找不到代码实现

AI：功能对应分析：

📋 设计功能：用户密码重置

🔍 代码搜索结果：
- 未找到 reset_password() 函数
- 未找到 /api/auth/reset-password 接口

💡 可能原因：
1. 功能尚未实现
2. 功能命名与设计不一致
3. 功能在其他模块中实现

🔎 相似功能搜索：
找到以下可能相关的代码：
- src/auth/service.py:156 - change_password()
- src/user/service.py:89 - update_password()

建议：
1. 确认change_password()是否实现了密码重置功能
2. 如功能未实现，参考设计文档实现
3. 如已实现，建议重命名函数以与设计一致
```

## 相关资源

### 子Skills

- **harness-design**: 需求与设计阶段
- **harness-coding**: 编码实现阶段
- **code-design-verify**: 代码-设计一致性验证
- **harness-testing**: 测试验证阶段
- **harness-quality**: 质量保证阶段
- **harness-deploy**: 构建部署阶段

### 模板文件

- [设计文档模板](./templates/design-template.md)
- [测试报告模板](./templates/test-report-template.md)
- [质量报告模板](./templates/quality-report-template.md)
- [部署记录模板](./templates/deploy-record-template.md)
- [代码-设计一致性报告模板](./templates/consistency-report-template.md)

### 参考文档

- [Harness开发规范](./references/coding-standards.md)
- [测试最佳实践](./references/testing-best-practices.md)
- [质量检查指南](./references/quality-checklist.md)
- [部署流程指南](./references/deployment-guide.md)
- [设计一致性验证指南](./references/design-consistency-guide.md)

## 使用建议

1. **新项目启动**：使用完整的5阶段流程
2. **功能开发**：从设计阶段开始，编码后自动验证一致性
3. **代码维护**：直接进入质量检查阶段
4. **问题修复**：从测试阶段开始验证
5. **设计变更**：更新设计文档后重新验证一致性

---

**版本**: 1.1.0  
**最后更新**: 2026-05-29
