# Harness工程开发模式 - 配置模板

## 完整配置文件模板

### .harness/config.yaml

```yaml
# Harness工程开发模式配置文件
# 版本: 1.0.0

# 项目基本信息
project:
  name: 项目名称
  version: 1.0.0
  description: 项目描述
  language: python  # python, java, javascript, go, etc.
  
# 开发流程配置
workflow:
  # 流程模式
  mode: standard  # standard, agile, waterfall
  
  # 自动流转
  auto_proceed: true
  
  # 质量门禁
  quality_gate: true
  
  # 代码评审
  require_review: true
  
  # 最少评审人数
  min_reviewers: 2

# 阶段配置
stages:
  # 设计阶段
  design:
    enabled: true
    auto_proceed_to_coding: false
    
    # 设计文档模板
    templates:
      - architecture.md
      - api-design.md
      - data-model.md
      
    # 设计评审
    review_required: true
    reviewers:
      - tech-lead
      - architect
  
  # 编码阶段
  coding:
    enabled: true
    
    # 编码规范
    standards: clean-code
    
    # 代码评审
    review_required: true
    
    # TDD模式
    tdd_enabled: true
    
    # 自动格式化
    auto_format: true
    
    # 提交前检查
    pre_commit_hooks:
      - lint
      - test
      - coverage
  
  # 测试阶段
  testing:
    enabled: true
    
    # 测试类型
    test_types:
      - unit
      - integration
      - e2e
      - performance
    
    # 覆盖率阈值
    coverage_threshold: 80
    
    # 并行执行
    parallel: true
    
    # 失败重试次数
    retry_count: 2
  
  # 质量阶段
  quality:
    enabled: true
    
    # 质量检查工具
    tools:
      - sonarqube
      - checkstyle
      - security-scan
      - dependency-check
    
    # 复杂度限制
    complexity_limit: 10
    
    # 重复代码率
    duplication_limit: 5
  
  # 部署阶段
  deploy:
    enabled: true
    
    # 部署环境
    environments:
      - name: dev
        auto_deploy: true
        strategy: rolling
        replicas: 2
        
      - name: test
        auto_deploy: false
        strategy: rolling
        replicas: 2
        
      - name: staging
        auto_deploy: false
        require_approval: true
        strategy: rolling
        replicas: 3
        
      - name: prod
        auto_deploy: false
        require_approval: true
        strategy: canary
        replicas: 10

# 质量标准
quality:
  # 代码覆盖率
  code_coverage: 80
  
  # 测试通过率
  test_pass_rate: 95
  
  # 代码复杂度
  complexity_limit: 10
  
  # 重复代码率
  duplication_limit: 5
  
  # 安全漏洞
  security_issues:
    critical: 0
    high: 0
    medium: 2
    low: 5

# 质量门禁规则
quality_gates:
  - name: 代码覆盖率
    metric: code_coverage
    threshold: 80
    operator: ">="
    
  - name: 测试通过率
    metric: test_pass_rate
    threshold: 95
    operator: ">="
    
  - name: 高危漏洞数
    metric: high_severity_issues
    threshold: 0
    operator: "=="
    
  - name: 代码复杂度
    metric: cyclomatic_complexity
    threshold: 10
    operator: "<="
    
  - name: 重复代码率
    metric: code_duplication
    threshold: 5
    operator: "<="

# 通知配置
notifications:
  # 邮件通知
  email:
    enabled: true
    recipients:
      - team@example.com
    events:
      - stage_completed
      - quality_gate_failed
      - deployment_completed
  
  # Slack通知
  slack:
    enabled: true
    webhook_url: ${SLACK_WEBHOOK_URL}
    channel: "#dev-team"
    events:
      - deployment_completed
      - production_issue
  
  # 企业微信通知
  wechat:
    enabled: true
    webhook_url: ${WECHAT_WEBHOOK_URL}
    events:
      - deployment_completed
      - production_issue

# 报告配置
reports:
  # 报告存储路径
  output_dir: reports
  
  # 报告保留天数
  retention_days: 30
  
  # 报告格式
  formats:
    - html
    - json
    - pdf

# 集成配置
integrations:
  # Git集成
  git:
    provider: github  # github, gitlab, bitbucket
    repository: owner/repo
    
  # CI/CD集成
  cicd:
    provider: harness  # harness, jenkins, gitlab-ci
    pipelines:
      build: build_pipeline
      deploy: deploy_pipeline
      test: test_pipeline
  
  # 代码质量平台
  quality_platform:
    provider: sonarqube
    url: https://sonar.example.com
    project_key: my-project
    
  # 监控平台
  monitoring:
    provider: prometheus
    url: https://prometheus.example.com
    grafana_url: https://grafana.example.com
```

### .harness/templates/design-template.md

```markdown
# 功能名称 - 技术设计文档

## 文档信息
- **版本**: v1.0
- **作者**: [作者姓名]
- **日期**: YYYY-MM-DD
- **状态**: 草稿/评审中/已批准

## 1. 概述

### 1.1 背景
描述功能的背景和业务价值。

### 1.2 目标
明确设计目标和成功指标。

### 1.3 范围
定义功能范围和边界。

## 2. 需求分析

### 2.1 功能需求
列出所有功能需求：
- 需求1
- 需求2

### 2.2 非功能需求

#### 性能需求
- 响应时间：XXXms
- 并发用户：XXX

#### 安全需求
- 认证方式：XXX
- 数据加密：XXX

#### 可用性需求
- 可用性：XX%
- 故障恢复时间：XXX

### 2.3 验收条件
使用EARS格式定义验收条件：

**场景1：**
- GIVEN [前置条件]
- WHEN [触发动作]
- THEN [预期结果]

## 3. 架构设计

### 3.1 系统架构

```
┌──────────────┐
│   前端层     │
└──────┬───────┘
       │
┌──────▼───────┐
│   API层      │
└──────┬───────┘
       │
┌──────▼───────┐
│  业务逻辑层  │
└──────┬───────┘
       │
┌──────▼───────┐
│   数据层     │
└──────────────┘
```

### 3.2 模块设计

| 模块名 | 职责 | 接口 |
|--------|------|------|
| 模块A | XXX | XXX |

### 3.3 技术选型

| 技术 | 版本 | 选择理由 |
|------|------|----------|
| 技术A | vX.X | XXX |

## 4. 接口设计

### 4.1 API接口

#### 接口1：功能名称

**请求**：
```
POST /api/v1/resource
```

**参数**：
| 参数名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| param1 | string | 是 | XXX |

**响应**：
```json
{
  "code": 200,
  "message": "success",
  "data": {}
}
```

### 4.2 错误码

| 错误码 | 说明 |
|--------|------|
| 400 | 参数错误 |
| 401 | 未授权 |

## 5. 数据模型

### 5.1 数据库设计

#### 表名：table_name

| 字段名 | 类型 | 约束 | 说明 |
|--------|------|------|------|
| id | UUID | PK | 主键 |

### 5.2 ER图

```
[实体A] --1:N--> [实体B]
```

## 6. 非功能设计

### 6.1 性能设计
- 性能指标
- 优化方案

### 6.2 安全设计
- 认证授权
- 数据安全

### 6.3 可观测性
- 日志规范
- 监控指标
- 告警规则

## 7. 风险与依赖

### 7.1 技术风险
| 风险 | 影响 | 应对措施 |
|------|------|----------|
| 风险1 | 高 | XXX |

### 7.2 外部依赖
| 依赖 | 版本 | 联系人 |
|------|------|--------|
| 服务A | vX.X | XXX |

## 8. 实施计划

### 8.1 开发计划
| 任务 | 负责人 | 预计时间 |
|------|--------|----------|
| 任务1 | XXX | X天 |

### 8.2 测试计划
- 测试策略
- 测试环境

### 8.3 发布计划
- 发布步骤
- 回滚方案

## 附录

### 术语表
| 术语 | 说明 |
|------|------|
| 术语1 | XXX |

### 参考文档
- [文档1](url)

### 变更历史
| 版本 | 日期 | 修改人 | 修改内容 |
|------|------|--------|----------|
| v1.0 | YYYY-MM-DD | XXX | 初始版本 |
```

### .harness/templates/test-report-template.md

```markdown
# 测试报告

## 测试概览

- **测试时间**: YYYY-MM-DD HH:MM:SS
- **测试环境**: [环境名称]
- **测试版本**: vX.X.X
- **测试执行人**: [姓名]

## 测试统计

### 总体统计

| 指标 | 数值 |
|------|------|
| 总测试数 | XXX |
| 通过 | XXX |
| 失败 | XXX |
| 跳过 | XXX |
| 通过率 | XX% |
| 执行时间 | XX秒 |

### 模块统计

| 模块 | 测试数 | 通过 | 失败 | 覆盖率 |
|------|--------|------|------|--------|
| 模块A | XX | XX | XX | XX% |

## 覆盖率报告

### 总体覆盖率

- **行覆盖率**: XX%
- **分支覆盖率**: XX%
- **函数覆盖率**: XX%

### 模块覆盖率

| 模块 | 行覆盖率 | 分支覆盖率 | 未覆盖行 |
|------|----------|------------|----------|
| 模块A | XX% | XX% | XX |

## 失败测试详情

### 测试1：test_function_name

**文件**: test_file.py:XX

**错误类型**: AssertionError

**错误信息**:
```
详细错误信息
```

**原因分析**:
- 原因1
- 原因2

**修复建议**:
```python
# 建议的修复代码
```

## 性能测试结果

### 响应时间

| 接口 | 平均 | P95 | P99 | 最大 |
|------|------|-----|-----|------|
| /api/v1/xxx | XXms | XXms | XXms | XXms |

### 并发测试

- 并发用户数: XX
- 平均响应时间: XXms
- 错误率: XX%

## 改进建议

### 短期改进

1. [改进建议1]
2. [改进建议2]

### 长期改进

1. [改进建议1]
2. [改进建议2]

## 结论

[测试结论和下一步建议]
```

### .harness/templates/quality-report-template.md

```markdown
# 质量报告

## 报告信息

- **报告时间**: YYYY-MM-DD HH:MM:SS
- **项目名称**: [项目名]
- **版本**: vX.X.X
- **代码行数**: XXXX

## 质量评分

**总分**: XX/100

**评级**: 优秀/良好/合格/不合格

## 质量指标

### 代码质量

| 指标 | 当前值 | 目标值 | 状态 |
|------|--------|--------|------|
| 代码覆盖率 | XX% | ≥80% | ✓/✗ |
| 代码复杂度 | XX | ≤10 | ✓/✗ |
| 重复代码率 | XX% | ≤5% | ✓/✗ |
| 技术债务 | XXh | ≤4h | ✓/✗ |

### 安全质量

| 指标 | 当前值 | 目标值 | 状态 |
|------|--------|--------|------|
| 高危漏洞 | XX | 0 | ✓/✗ |
| 中危漏洞 | XX | ≤2 | ✓/✗ |
| 低危漏洞 | XX | ≤5 | ✓/✗ |

### 测试质量

| 指标 | 当前值 | 目标值 | 状态 |
|------|--------|--------|------|
| 测试通过率 | XX% | ≥95% | ✓/✗ |
| 单元测试数 | XX | - | - |
| 集成测试数 | XX | - | - |

## 问题清单

### 高优先级问题

1. **[问题类型]** - [问题描述]
   - 位置: file.py:XX
   - 影响: XXX
   - 建议: XXX

### 中优先级问题

1. **[问题类型]** - [问题描述]
   - 位置: file.py:XX

### 低优先级问题

1. **[问题类型]** - [问题描述]
   - 位置: file.py:XX

## 安全漏洞详情

### CVE-XXXX-XXXX

- **严重度**: 高危/中危/低危
- **CVSS分数**: X.X
- **影响组件**: XXX vX.X.X
- **漏洞描述**: XXX
- **修复方案**: 升级到 vX.X.X

## 质量门禁

| 规则 | 阈值 | 实际值 | 状态 |
|------|------|--------|------|
| 代码覆盖率 | ≥80% | XX% | ✓/✗ |
| 测试通过率 | ≥95% | XX% | ✓/✗ |
| 高危漏洞数 | =0 | XX | ✓/✗ |

**门禁状态**: 通过/不通过

## 改进建议

1. [建议1]
2. [建议2]
3. [建议3]

## 附录

- 详细报告: [链接]
- 历史趋势: [链接]
```

---

## 使用说明

1. 复制配置模板到项目根目录：`.harness/config.yaml`
2. 根据项目实际情况修改配置
3. 各阶段会自动读取配置并执行

---

**版本**: 1.0.0  
**最后更新**: 2026-05-28
