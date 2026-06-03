# Harness Integration Skill

## 简介

将Harness的CI/CD能力集成到OpenCode中，实现代码质量检查、自动化测试、构建部署的深度集成。

## 功能特性

- **代码质量检查**：自动触发代码扫描，查看质量报告
- **自动化测试**：运行单元测试、集成测试，分析测试结果
- **构建部署**：触发构建流程，部署到不同环境
- **质量门禁**：检查质量门禁，提供改进建议
- **流水线监控**：查看流水线状态和执行日志

## 安装

### 方法1：复制到OpenCode Skills目录

```bash
cp -r harness-integration ~/.opencode/skills/
```

### 方法2：使用符号链接

```bash
ln -s $(pwd)/harness-integration ~/.opencode/skills/
```

## 配置

### 1. 配置环境变量

```bash
export HARNESS_API_KEY="your-api-key"
export HARNESS_ACCOUNT_ID="your-account-id"
export HARNESS_ORG_ID="your-org-id"
export HARNESS_PROJECT_ID="your-project-id"
```

### 2. 创建配置文件

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
  build: build_pipeline
  deploy_dev: deploy_to_dev
```

## 使用方法

### 代码质量检查

```
用户：检查当前代码质量
AI：[自动触发代码扫描，返回质量报告]
```

### 运行测试

```
用户：运行单元测试
AI：[自动触发测试，返回测试报告]
```

### 部署应用

```
用户：部署到开发环境
AI：[自动触发部署，返回部署结果]
```

## 配置文件示例

参考 `templates/harness-config-template.yaml`

## 最佳实践

参考 `references/best-practices.md`

## 故障排查

参考 `SKILL.md` 中的故障排查章节

## 相关链接

- [Harness官方文档](https://developer.harness.io)
- [OpenCode文档](https://opencode.ai)
