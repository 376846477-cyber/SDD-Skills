---
name: harness-integration
description: Harness CI/CD集成Skill - 在OpenCode中享受Harness的持续集成和持续交付能力。适用场景：(1) 代码质量检查；(2) 自动化测试；(3) 构建部署；(4) 质量门禁管理。触发关键词：质量检查、测试、部署、发布、流水线、harness、CI/CD、代码扫描、单元测试
---

# Harness Integration Skill

## 问题背景

现代软件开发需要高质量的CI/CD流程，但开发人员往往需要：
- 在多个平台间切换
- 手动触发流水线
- 查看分散的测试报告
- 处理复杂的部署流程

**核心解决方案：OpenCode + Harness深度集成**

```
开发人员在OpenCode中编码 → 触发Harness流水线 → 实时查看结果 → 获得AI辅助建议
```

---

## 快速开始

### 使用方法

```
用户：检查当前代码质量
AI：[自动触发harness-integration Skill]
    1. 触发Harness代码扫描流水线
    2. 等待扫描完成
    3. 返回质量报告和AI修复建议
```

```
用户：运行单元测试
AI：[自动触发harness-integration Skill]
    1. 触发Harness测试流水线
    2. 监控测试执行
    3. 返回测试报告和失败分析
```

```
用户：部署到开发环境
AI：[自动触发harness-integration Skill]
    1. 触发Harness部署流水线
    2. 监控部署进度
    3. 返回部署结果和访问地址
```

---

## 配置要求

### 步骤1：配置环境变量

```bash
# Linux/macOS
export HARNESS_API_KEY="your-api-key"
export HARNESS_ACCOUNT_ID="your-account-id"
export HARNESS_ORG_ID="your-org-id"
export HARNESS_PROJECT_ID="your-project-id"

# Windows (PowerShell)
$env:HARNESS_API_KEY="your-api-key"
$env:HARNESS_ACCOUNT_ID="your-account-id"
$env:HARNESS_ORG_ID="your-org-id"
$env:HARNESS_PROJECT_ID="your-project-id"
```

### 步骤2：创建配置文件

在项目根目录创建 `.opencode/harness-config.yaml`：

```yaml
harness:
  api_url: https://app.harness.io/api
  api_key: ${HARNESS_API_KEY}
  account_id: ${HARNESS_ACCOUNT_ID}
  organization_id: ${HARNESS_ORG_ID}
  project_id: ${HARNESS_PROJECT_ID}
  
pipelines:
  code_scan: code_scan_pipeline
  unit_test: unit_test_pipeline
  integration_test: integration_test_pipeline
  build: build_pipeline
  deploy_dev: deploy_to_dev
  deploy_prod: deploy_to_prod
  
quality_gates:
  code_coverage: 80
  test_pass_rate: 95
  security_scan: high
```

---

## 核心功能

### 1. 代码质量检查

**触发关键词**：质量检查、代码扫描、代码质量

**功能**：
- 自动触发代码扫描流水线
- 查看代码质量报告
- 获得AI修复建议

**示例**：
```
用户：检查当前代码质量

AI：正在触发代码扫描...
✓ 扫描完成

质量报告：
- 代码覆盖率: 85%
- 代码复杂度: 中等
- 安全漏洞: 2个高危

修复建议：
1. 修复CVE-2024-1234 (src/auth.py:45)
2. 降低函数复杂度 (src/calculator.py:200)
```

### 2. 自动化测试

**触发关键词**：测试、单元测试、集成测试

**功能**：
- 触发单元测试、集成测试
- 查看测试报告
- 分析失败原因

**示例**：
```
用户：运行单元测试

AI：正在运行测试...
✓ 测试完成

测试报告：
- 总测试数: 122
- 通过: 120
- 失败: 2
- 覆盖率: 85%

失败分析：
1. test_notification.py::test_send_email - AssertionError
   原因：邮件服务配置错误
   建议：检查src/notification.py:100
```

### 3. 构建部署

**触发关键词**：构建、部署、发布

**功能**：
- 触发构建流程
- 部署到不同环境
- 查看部署状态

**示例**：
```
用户：部署到开发环境

AI：正在部署...
✓ 部署成功

部署信息：
- 环境: dev
- 版本: v1.2.3
- URL: https://dev.myapp.example.com
- 状态: 运行中
```

### 4. 质量门禁

**触发关键词**：质量门禁、检查门禁

**功能**：
- 检查质量门禁状态
- 查看不通过原因
- 获得改进建议

**示例**：
```
用户：检查质量门禁

AI：质量门禁状态：

✓ 代码覆盖率: 85% (达标, >= 80%)
✓ 测试通过率: 98% (达标, >= 95%)
✗ 安全扫描: 2个高危漏洞 (不达标)

建议修复：
1. 修复CVE-2024-1234
2. 修复CVE-2024-5678
```

### 5. 流水线监控

**触发关键词**：流水线状态、查看流水线

**功能**：
- 查看流水线执行状态
- 查看执行日志
- 列出所有流水线

**示例**：
```
用户：查看流水线状态

AI：流水线列表：

1. code_scan_pipeline (最近执行: 成功)
2. unit_test_pipeline (最近执行: 成功)
3. build_pipeline (最近执行: 失败)
4. deploy_dev_pipeline (最近执行: 成功)

执行中: 0
最近24小时成功率: 95%
```

---

## 处理流程

### 流程图

```
用户请求
    ↓
解析请求类型
    ├─ 质量检查 → trigger_code_scan()
    ├─ 测试 → trigger_test()
    ├─ 构建 → trigger_build()
    ├─ 部署 → trigger_deploy()
    └─ 查看状态 → get_status()
    ↓
调用Harness API
    ↓
等待执行完成
    ↓
获取结果
    ↓
AI分析并提供改进建议
    ↓
返回给用户
```

### 决策逻辑

```python
def handle_request(user_input):
    # 识别请求类型
    if any(keyword in user_input for keyword in ['质量检查', '代码扫描', '代码质量']):
        return trigger_code_scan()
    elif any(keyword in user_input for keyword in ['测试', '单元测试', '集成测试']):
        return trigger_test()
    elif any(keyword in user_input for keyword in ['构建', 'build']):
        return trigger_build()
    elif any(keyword in user_input for keyword in ['部署', '发布', 'deploy']):
        return trigger_deploy()
    elif any(keyword in user_input for keyword in ['流水线', '状态', '查看']):
        return get_status()
```

---

## 最佳实践

### 1. 提交前检查

```
用户：帮我检查代码质量，准备提交

AI：正在执行提交前检查...
1. 代码扫描 ✓
2. 单元测试 ✓
3. 质量门禁 ✓

所有检查通过，可以提交！
```

### 2. 持续集成

```
用户：提交代码后自动运行测试

AI：已配置CI流水线：
- 触发条件: push到任意分支
- 执行步骤: 代码扫描 → 单元测试 → 质量门禁
- 失败通知: Slack + Email
```

### 3. 环境部署

```
用户：部署到开发环境

AI：自动部署流程：
1. 拉取最新代码
2. 构建Docker镜像
3. 运行集成测试
4. 部署到dev环境
5. 健康检查

✓ 部署成功！访问: https://dev.myapp.example.com
```

---

## 故障排查

### 问题1：API连接失败

**解决方案**：
```bash
# 检查API密钥
echo $HARNESS_API_KEY

# 测试连接
curl -H "Authorization: Bearer $HARNESS_API_KEY" \
  https://app.harness.io/api/users/current
```

### 问题2：流水线执行失败

**解决方案**：
```
用户：为什么流水线失败了？

AI：失败原因分析：
1. 单元测试失败 (test_user_api.py:45)
2. 原因: AssertionError - 期望值不匹配
3. 建议: 检查测试数据和断言条件

是否需要查看详细日志？
```

### 问题3：质量门禁不通过

**解决方案**：
```
用户：如何通过质量门禁？

AI：质量门禁要求：
✗ 代码覆盖率: 75% < 80%

改进建议：
1. 为Calculator类添加测试
2. 为UserService类添加测试
3. 预计可提升覆盖率至85%

是否生成测试代码？
```

---

## 相关资源

- [Harness官方文档](https://developer.harness.io)
- [OpenCode文档](https://opencode.ai)
- [配置文件模板](./templates/harness-config-template.yaml)
- [API参考文档](./references/harness-api-reference.md)
- [最佳实践指南](./references/best-practices.md)
