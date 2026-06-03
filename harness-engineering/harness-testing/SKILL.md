---
name: harness-testing
description: Harness测试阶段Skill - 管理软件测试流程和质量验证。包含单元测试、集成测试、测试报告生成、覆盖率分析、测试失败分析。触发关键词：运行测试、测试报告、测试流程、覆盖率、集成测试、单元测试、testing
---

# Harness测试阶段

## 阶段概述

测试阶段是确保软件质量的关键环节，通过系统化的测试流程验证功能正确性、性能指标和稳定性。本阶段支持多种测试类型，提供详细的测试报告和失败分析，帮助团队快速定位和修复问题。

## 测试类型

### 1. 单元测试

**定义**：测试单个函数或类的行为

**目标**：
- 验证函数逻辑正确性
- 保证代码可测试性
- 提高代码覆盖率

**最佳实践**：
- 每个测试独立运行
- 使用Mock隔离依赖
- 测试命名清晰描述场景

### 2. 集成测试

**定义**：测试模块间的交互

**目标**：
- 验证模块集成正确性
- 测试接口契约
- 验证数据流

**测试范围**：
- API接口测试
- 数据库集成测试
- 第三方服务集成测试

### 3. 端到端测试

**定义**：测试完整业务流程

**目标**：
- 验证用户场景
- 测试系统整体行为
- 模拟真实用户操作

**测试方式**：
- UI自动化测试
- API链路测试
- 业务流程测试

### 4. 性能测试

**定义**：测试系统性能指标

**目标**：
- 验证响应时间
- 测试并发处理能力
- 识别性能瓶颈

**测试类型**：
- 负载测试
- 压力测试
- 并发测试
- 基准测试

## 测试流程

### 标准测试流程

```
测试计划
    ↓
测试用例设计
    ├─ 正常场景
    ├─ 边界场景
    └─ 异常场景
    ↓
测试执行
    ├─ 单元测试
    ├─ 集成测试
    └─ 端到端测试
    ↓
结果分析
    ├─ 测试报告
    ├─ 覆盖率分析
    └─ 失败分析
    ↓
问题修复
    └─ 修复并重新测试
    ↓
测试通过
    └─ 生成测试报告
```

### 测试执行策略

```python
class TestStrategy:
    """测试执行策略"""
    
    def execute_tests(self):
        # 1. 快速反馈：先运行单元测试
        unit_results = self.run_unit_tests()
        
        # 2. 模块集成：运行集成测试
        if unit_results.pass_rate >= 0.95:
            integration_results = self.run_integration_tests()
        else:
            return "单元测试通过率不足，请先修复"
        
        # 3. 业务验证：运行端到端测试
        if integration_results.pass_rate >= 0.90:
            e2e_results = self.run_e2e_tests()
        else:
            return "集成测试通过率不足，请先修复"
        
        # 4. 性能验证：运行性能测试
        if e2e_results.pass_rate >= 0.85:
            perf_results = self.run_performance_tests()
        
        return self.generate_report([
            unit_results,
            integration_results,
            e2e_results,
            perf_results
        ])
```

## 使用示例

### 场景1：运行单元测试

```
用户：运行所有单元测试

AI：[触发harness-testing]
正在执行单元测试...

📊 测试执行进度

[1/3] 运行test_user_service.py...
✓ test_create_user_success
✓ test_create_user_with_invalid_email
✓ test_create_user_with_duplicate_email
✓ test_update_user_profile
✓ test_delete_user
─────────────────────
通过：5/5

[2/3] 运行test_auth_service.py...
✓ test_login_success
✓ test_login_invalid_password
✓ test_login_user_not_found
✗ test_login_with_locked_account
─────────────────────
通过：3/4

[3/3] 运行test_order_service.py...
✓ test_create_order
✓ test_cancel_order
✓ test_get_order_by_id
─────────────────────
通过：3/3

━━━━━━━━━━━━━━━━━━━━━

📊 测试报告

总览：
- 总测试数：12
- 通过：11
- 失败：1
- 跳过：0
- 执行时间：2.34秒

通过率：91.7%

━━━━━━━━━━━━━━━━━━━━━

📈 覆盖率报告

文件覆盖率：
┌─────────────────────┬────────┬─────────┐
│ 文件                 │ 覆盖率 │ 未覆盖行 │
├─────────────────────┼────────┼─────────┤
│ user_service.py     │ 95%    │ 3       │
│ auth_service.py     │ 88%    │ 8       │
│ order_service.py    │ 100%   │ 0       │
├─────────────────────┼────────┼─────────┤
│ 总覆盖率             │ 92%    │ 11      │
└─────────────────────┴────────┴─────────┘

未覆盖代码详情：
auth_service.py:45-52 - 账户锁定逻辑
user_service.py:120-122 - 异常处理分支

━━━━━━━━━━━━━━━━━━━━━

❌ 失败测试分析

测试：test_login_with_locked_account
文件：test_auth_service.py:45

错误信息：
AssertionError: Expected error message '账户已锁定', got '登录成功'

原因分析：
1. 账户锁定状态检查逻辑缺失
2. login()方法未验证账户状态

代码位置：
auth_service.py:78 - login()方法

建议修复：
```python
def login(self, email: str, password: str) -> Dict:
    user = self.user_repo.find_by_email(email)
    
    # 添加账户状态检查
    if user.status == UserStatus.LOCKED:
        return {
            'success': False,
            'error': '账户已锁定'
        }
    
    # 原有逻辑...
```

━━━━━━━━━━━━━━━━━━━━━

💡 后续建议

1. 修复失败测试：test_login_with_locked_account
2. 提高覆盖率：补充账户锁定相关测试
3. 代码评审：检查账户状态管理逻辑

测试报告已保存：reports/test-report-20260528.html
```

### 场景2：运行集成测试

```
用户：运行集成测试

AI：正在执行集成测试...

🔧 测试环境准备
- 启动测试数据库：PostgreSQL (test_db)
- 启动Redis：localhost:6379
- 启动测试服务：http://localhost:8080

━━━━━━━━━━━━━━━━━━━━━

📊 集成测试执行

[API测试] user_api_test.py
─────────────────────
POST /api/v1/users
  ✓ 创建用户 (201)
  ✓ 验证邮箱格式 (400)
  ✓ 重复邮箱注册 (409)

GET /api/v1/users/{id}
  ✓ 获取用户信息 (200)
  ✓ 用户不存在 (404)
  ✓ 权限验证 (403)

PUT /api/v1/users/{id}
  ✓ 更新用户信息 (200)
  ✓ 无效参数 (400)

─────────────────────
通过：8/8

[数据库测试] database_test.py
─────────────────────
✓ 用户表CRUD操作
✓ 订单表关联查询
✓ 事务回滚测试
✓ 并发写入测试

─────────────────────
通过：4/4

[外部服务测试] integration_test.py
─────────────────────
✓ 邮件服务集成
✗ 支付服务集成 - 连接超时
✓ 短信服务集成

─────────────────────
通过：2/3

━━━━━━━━━━━━━━━━━━━━━

📊 集成测试报告

总览：
- 测试套件：3
- 总测试数：15
- 通过：14
- 失败：1
- 执行时间：45.6秒

环境信息：
- 数据库：PostgreSQL 14.2
- Python：3.11.0
- 测试框架：pytest 7.4.3

━━━━━━━━━━━━━━━━━━━━━

❌ 失败测试详情

测试：test_payment_service_integration
套件：integration_test.py:120

错误类型：ConnectionTimeout
错误信息：PaymentService连接超时，等待30秒后失败

原因分析：
1. 支付服务未启动或不可达
2. 网络配置问题
3. 服务端负载过高

环境检查：
✓ 配置文件：存在
✓ 服务地址：https://payment.test.example.com
✗ 服务健康检查：失败

建议修复：
1. 检查支付服务是否启动
2. 验证网络连接：curl https://payment.test.example.com/health
3. 检查服务日志

是否需要使用Mock支付服务进行测试？
```

### 场景3：性能测试

```
用户：运行性能测试

AI：正在执行性能测试...

📊 测试配置

测试类型：负载测试
并发用户：100
持续时间：60秒
目标接口：POST /api/v1/orders

━━━━━━━━━━━━━━━━━━━━━

📈 测试执行中...

预热阶段 (10秒)
─────────────────────
并发用户：0 → 50
平均响应时间：45ms
成功率：100%

负载阶段 (40秒)
─────────────────────
并发用户：50 → 100
平均响应时间：85ms
P95响应时间：145ms
P99响应时间：210ms
成功率：99.8%

冷却阶段 (10秒)
─────────────────────
并发用户：100 → 0
平均响应时间：75ms
成功率：100%

━━━━━━━━━━━━━━━━━━━━━

📊 性能测试报告

总体统计：
- 总请求数：12,450
- 成功请求：12,425
- 失败请求：25
- 总测试时间：60.3秒

性能指标：
┌──────────────────┬─────────┬─────────┐
│ 指标              │ 实际值   │ 目标值  │
├──────────────────┼─────────┼─────────┤
│ 平均响应时间      │ 85ms    │ <100ms  │
│ P95响应时间       │ 145ms   │ <200ms  │
│ P99响应时间       │ 210ms   │ <500ms  │
│ 吞吐量            │ 207 RPS │ >200 RPS│
│ 错误率            │ 0.2%    │ <1%     │
└──────────────────┴─────────┴─────────┘

性能评估：✅ 通过

━━━━━━━━━━━━━━━━━━━━━

📊 响应时间分布

  0-50ms   : ████████████ 45%
  50-100ms : ██████████ 35%
  100-150ms: ████ 12%
  150-200ms: ██ 5%
  200-500ms: █ 2%
  >500ms   : ▌ 1%

━━━━━━━━━━━━━━━━━━━━━

⚠ 性能问题分析

发现的问题：
1. 响应时间在并发100时略有上升
2. 1%的请求响应时间超过500ms
3. 25个请求失败（连接超时）

瓶颈分析：
1. 数据库连接池达到上限
   - 当前配置：max_connections=100
   - 建议：增加到200

2. 订单创建接口存在慢查询
   - 位置：order_service.py:89
   - 建议：优化索引或增加缓存

💡 优化建议

短期优化：
1. 增加数据库连接池大小
2. 添加订单查询索引
3. 实现接口限流

中期优化：
1. 引入缓存层
2. 订单创建异步化
3. 数据库读写分离

━━━━━━━━━━━━━━━━━━━━━

📄 报告已生成：
- HTML报告：reports/performance-20260528.html
- JSON数据：reports/performance-20260528.json
- 图表：reports/performance-charts-20260528/

是否需要运行压力测试？
```

## 测试报告模板

### 单元测试报告

```markdown
# 单元测试报告

## 测试概览

- 测试时间：2026-05-28 10:30:00
- 测试环境：Python 3.11.0
- 测试框架：pytest 7.4.3
- 执行时间：2.34秒

## 测试统计

| 指标 | 数值 |
|------|------|
| 总测试数 | 120 |
| 通过 | 118 |
| 失败 | 2 |
| 跳过 | 0 |
| 通过率 | 98.3% |

## 覆盖率报告

| 模块 | 覆盖率 | 未覆盖行 |
|------|--------|----------|
| user_service | 95% | 5 |
| auth_service | 92% | 8 |
| order_service | 100% | 0 |
| **总计** | **95%** | **13** |

## 失败测试详情

### test_user_login_with_locked_account

**文件**：test_auth_service.py:45
**错误**：AssertionError
**预期**：返回账户已锁定错误
**实际**：返回登录成功

**修复建议**：
在login方法中添加账户状态检查。

## 改进建议

1. 补充账户锁定相关测试用例
2. 提高auth_service覆盖率至95%以上
3. 修复失败的测试用例
```

## 测试最佳实践

### 测试数据管理

```python
import pytest
from factory import Factory, Faker

class UserFactory(Factory):
    """测试数据工厂"""
    
    email = Faker('email')
    name = Faker('name')
    age = Faker('random_int', min=18, max=80)
    
    class Meta:
        model = User

# 使用示例
def test_create_user():
    user_data = UserFactory.build()  # 构建但不保存
    user = UserFactory.create()       # 构建并保存
```

### Mock使用

```python
from unittest.mock import Mock, patch

def test_send_email():
    # Mock邮件服务
    with patch('services.email.send') as mock_send:
        mock_send.return_value = {'success': True}
        
        result = send_welcome_email('user@example.com')
        
        # 验证调用
        mock_send.assert_called_once_with(
            to='user@example.com',
            subject='欢迎',
            body='欢迎加入我们！'
        )
```

### 参数化测试

```python
import pytest

@pytest.mark.parametrize("input,expected", [
    (0, 0),
    (1, 1),
    (10, 55),
    (-1, None),
])
def test_fibonacci(input, expected):
    result = fibonacci(input)
    assert result == expected
```

## 测试清单

### 单元测试清单

- [ ] 测试命名清晰描述测试场景
- [ ] 每个测试只验证一个行为
- [ ] 使用AAA模式
- [ ] 测试数据使用工厂模式
- [ ] 外部依赖使用Mock
- [ ] 测试覆盖正常、边界、异常场景
- [ ] 测试执行独立，不依赖顺序

### 集成测试清单

- [ ] 测试环境隔离
- [ ] 数据库使用测试数据库
- [ ] 测试前后清理数据
- [ ] 测试事务正确性
- [ ] 测试并发场景
- [ ] 测试错误处理

### 性能测试清单

- [ ] 定义性能基准
- [ ] 设置合理的负载模型
- [ ] 监控系统资源
- [ ] 分析性能瓶颈
- [ ] 记录测试结果趋势

## 相关资源

- [测试最佳实践](./references/testing-best-practices.md)
- [Mock使用指南](./references/mock-guide.md)
- [性能测试指南](./references/performance-testing.md)

---

**版本**: 1.0.0  
**最后更新**: 2026-05-28
