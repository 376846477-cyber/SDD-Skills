---
name: harness-quality
description: Harness质量阶段Skill - 管理代码质量检查和质量门禁。包含代码规范检查、静态分析、安全扫描、性能分析、质量门禁验证。触发关键词：质量检查、代码质量、质量门禁、静态分析、安全扫描、quality
---

# Harness质量阶段

## 阶段概述

质量阶段通过系统化的质量检查流程，确保代码满足质量标准和安全要求。通过静态分析、安全扫描、性能分析等多维度检查，在代码合并前发现并修复潜在问题，实现"质量左移"。

## 核心活动

### 1. 代码规范检查

**目标**：确保代码符合团队编码规范

**检查内容**：
- 代码格式化
- 命名规范
- 注释规范
- 代码结构
- 最佳实践

**工具支持**：
- Python: pylint, flake8, black
- JavaScript: ESLint, Prettier
- Java: Checkstyle, PMD
- Go: gofmt, golint

### 2. 静态分析

**目标**：在不运行代码的情况下发现潜在问题

**分析内容**：
- 代码复杂度
- 代码重复
- 潜在Bug
- 代码异味
- 技术债务

**工具支持**：
- SonarQube
- CodeClimate
- Fortify
- Coverity

### 3. 安全扫描

**目标**：识别代码中的安全漏洞

**扫描内容**：
- SQL注入
- XSS跨站脚本
- CSRF跨站请求伪造
- 敏感数据泄露
- 不安全的依赖

**工具支持**：
- OWASP Dependency-Check
- Snyk
- Checkmarx
- Veracode

### 4. 性能分析

**目标**：识别性能瓶颈和优化机会

**分析内容**：
- 响应时间分析
- 内存使用分析
- CPU使用分析
- 数据库查询分析
- 资源泄漏检测

**工具支持**：
- JProfiler (Java)
- cProfile (Python)
- Chrome DevTools (JavaScript)
- pprof (Go)

### 5. 质量门禁

**目标**：设置质量标准，阻止不合格代码合并

**门禁条件**：
- 代码覆盖率 ≥ 80%
- 测试通过率 ≥ 95%
- 零高危安全漏洞
- 代码复杂度 ≤ 10
- 重复代码率 ≤ 5%

## 质量检查流程

### 标准质量检查流程

```
代码提交
    ↓
代码规范检查
    ├─ 格式检查
    ├─ 命名检查
    └─ 注释检查
    ↓
静态分析
    ├─ 复杂度分析
    ├─ 重复代码检测
    └─ 潜在Bug检测
    ↓
安全扫描
    ├─ 代码安全扫描
    ├─ 依赖安全扫描
    └─ 敏感信息检查
    ↓
性能分析
    ├─ 响应时间分析
    ├─ 内存分析
    └─ 资源使用分析
    ↓
质量门禁判断
    ├─ 各项指标达标？
    ├─ YES → 允许合并
    └─ NO  → 阻止合并，返回问题
```

### 质量门禁决策

```python
class QualityGate:
    """质量门禁"""
    
    def __init__(self):
        self.rules = [
            QualityRule('代码覆盖率', 'code_coverage', 80, '>='),
            QualityRule('测试通过率', 'test_pass_rate', 95, '>='),
            QualityRule('高危漏洞数', 'high_severity_issues', 0, '=='),
            QualityRule('代码复杂度', 'complexity', 10, '<='),
            QualityRule('重复代码率', 'duplication', 5, '<='),
        ]
    
    def evaluate(self, metrics):
        """评估质量门禁"""
        results = []
        
        for rule in self.rules:
            value = metrics.get(rule.metric)
            passed = self._compare(value, rule.threshold, rule.operator)
            
            results.append({
                'rule': rule.name,
                'value': value,
                'threshold': rule.threshold,
                'operator': rule.operator,
                'passed': passed
            })
        
        all_passed = all(r['passed'] for r in results)
        
        return {
            'passed': all_passed,
            'results': results,
            'summary': self._generate_summary(results)
        }
```

## 使用示例

### 场景1：代码质量检查

```
用户：检查当前代码质量

AI：[触发harness-quality]
正在执行质量检查流程...

━━━━━━━━━━━━━━━━━━━━━

📋 第一步：代码规范检查

检查文件：src/auth_service.py

代码格式 ✓
- 缩进：使用4空格 ✓
- 行长度：最长98字符 ✓
- 空行：符合PEP8 ✓

命名规范 ✓
- 类名：AuthService (大驼峰) ✓
- 函数名：login_user (小写下划线) ✓
- 变量名：user_count (小写下划线) ✓

注释规范 ⚠
- 缺少模块文档字符串
- login()函数缺少参数说明

问题统计：
- 错误：0
- 警告：2
- 建议：5

━━━━━━━━━━━━━━━━━━━━━

📊 第二步：静态分析

使用SonarQube分析中...

代码复杂度：
┌─────────────┬────────┬─────────┐
│ 函数         │ 复杂度 │ 状态    │
├─────────────┼────────┼─────────┤
│ login()     │ 8      │ ✓ 正常  │
│ register()  │ 12     │ ⚠ 偏高  │
│ validate()  │ 5      │ ✓ 正常  │
└─────────────┴────────┴─────────┘

代码重复：
- 重复代码块：3个
- 重复代码行：45行
- 重复率：2.3% ✓

潜在Bug：
- 空指针风险：2处
- 资源未关闭：1处
- 异常未处理：3处

技术债务：
- 债务时间：2小时
- 主要问题：缺少单元测试

━━━━━━━━━━━━━━━━━━━━━

🔒 第三步：安全扫描

OWASP依赖检查：
- 检查依赖：127个
- 已知漏洞：3个

漏洞详情：
┌──────────┬────────┬──────────────────────┐
│ CVE编号   │ 严重度 │ 依赖包                │
├──────────┼────────┼──────────────────────┤
│ CVE-2024-1234 │ 高危 │ requests==2.28.0  │
│ CVE-2024-5678 │ 中危 │ flask==2.0.1     │
│ CVE-2024-9012 │ 低危 │ jinja2==3.0.1    │
└──────────┴────────┴──────────────────────┘

代码安全扫描：
- SQL注入风险：0处 ✓
- XSS风险：0处 ✓
- 硬编码密码：1处 ⚠
  位置：config.py:15

敏感信息检查：
- 发现疑似密钥：2处
- 位置：.env.example (示例文件)

━━━━━━━━━━━━━━━━━━━━━

⚡ 第四步：性能分析

响应时间分析：
- login(): 平均45ms ✓
- register(): 平均120ms ⚠

瓶颈识别：
1. register()方法存在N+1查询
   位置：auth_service.py:89
   影响：用户列表较大时响应慢

内存分析：
- 峰值内存：256MB ✓
- 内存泄漏：未发现 ✓

━━━━━━━━━━━━━━━━━━━━━

🚦 第五步：质量门禁

质量指标评估：

✓ 代码覆盖率：92% (>= 80%)
✓ 测试通过率：98% (>= 95%)
✗ 高危漏洞数：1 (> 0)
✓ 代码复杂度：8 (<= 10)
✓ 重复代码率：2.3% (<= 5%)

━━━━━━━━━━━━━━━━━━━━━

📊 质量报告总结

质量评分：85/100

质量状态：⚠ 需改进

必须修复：
1. 🔴 CVE-2024-1234 (高危漏洞)
   升级requests到2.31.0+
   
2. 🔴 硬编码密码
   位置：config.py:15
   移除硬编码，使用环境变量

建议改进：
1. 🟡 降低register()复杂度
2. 🟡 添加缺少的文档字符串
3. 🟡 修复N+1查询问题

质量报告已保存：
- reports/quality-report-20260528.html
- reports/quality-report-20260528.json

是否需要查看详细的修复建议？
```

### 场景2：质量门禁检查

```
用户：检查质量门禁状态

AI：正在评估质量门禁...

━━━━━━━━━━━━━━━━━━━━━

🚦 质量门禁状态

总体状态：✗ 不通过

━━━━━━━━━━━━━━━━━━━━━

详细评估：

1. 代码覆盖率
   当前值：75%
   目标值：>= 80%
   状态：✗ 不达标
   差距：-5%
   
   未覆盖模块：
   - user_service.py (70%)
   - notification_service.py (65%)
   
   建议：为上述模块补充单元测试

2. 测试通过率
   当前值：100%
   目标值：>= 95%
   状态：✓ 达标

3. 高危漏洞数
   当前值：0
   目标值：= 0
   状态：✓ 达标

4. 代码复杂度
   当前值：12
   目标值：<= 10
   状态：✗ 不达标
   
   高复杂度函数：
   - process_order() 复杂度：15
   - validate_payment() 复杂度：14
   
   建议：拆分复杂函数

5. 重复代码率
   当前值：3.2%
   目标值：<= 5%
   状态：✓ 达标

━━━━━━━━━━━━━━━━━━━━━

📋 不通过原因

1. 代码覆盖率不足 (75% < 80%)
2. 代码复杂度过高 (12 > 10)

━━━━━━━━━━━━━━━━━━━━━

💡 达标方案

方案A：提高代码覆盖率
```python
# 为user_service补充测试
class TestUserService:
    def test_create_user_with_invalid_email(self):
        """测试无效邮箱"""
        pass
    
    def test_update_user_profile(self):
        """测试更新用户资料"""
        pass
```

预计覆盖率提升：75% → 82%

方案B：降低代码复杂度
```python
# 拆分process_order函数
def process_order(order_id):
    order = validate_order(order_id)
    payment = process_payment(order)
    notify_user(order)
    return order

def validate_order(order_id):
    """验证订单"""
    pass

def process_payment(order):
    """处理支付"""
    pass
```

预计复杂度降低：15 → 8

是否应用上述改进方案？
```

### 场景3：安全漏洞修复

```
用户：帮我修复安全漏洞

AI：正在分析安全漏洞...

━━━━━━━━━━━━━━━━━━━━━

🔒 安全漏洞清单

高危漏洞 (1个)
─────────────────────
1. CVE-2024-1234
   类型：SQL注入
   严重度：高危
   CVSS：9.8
   影响：可导致数据泄露
   
   受影响代码：
   ```python
   # user_service.py:45
   def get_user(username):
       query = f"SELECT * FROM users WHERE username='{username}'"
       return db.execute(query)
   ```
   
   风险：攻击者可通过username参数注入SQL
   
   修复方案：
   ```python
   # 使用参数化查询
   def get_user(username):
       query = "SELECT * FROM users WHERE username = ?"
       return db.execute(query, (username,))
   ```

中危漏洞 (2个)
─────────────────────
1. CVE-2024-5678
   类型：XSS跨站脚本
   严重度：中危
   CVSS：6.1
   
   受影响代码：
   ```python
   # template.py:23
   def render_profile(user):
       return f"<div>{user.name}</div>"
   ```
   
   修复方案：
   ```python
   from markupsafe import escape
   
   def render_profile(user):
       return f"<div>{escape(user.name)}</div>"
   ```

2. 硬编码密码
   类型：敏感信息泄露
   严重度：中危
   
   受影响代码：
   ```python
   # config.py:15
   DB_PASSWORD = "mysecretpassword123"
   ```
   
   修复方案：
   ```python
   import os
   DB_PASSWORD = os.environ.get('DB_PASSWORD')
   ```

━━━━━━━━━━━━━━━━━━━━━

🛠 修复脚本

已生成自动修复脚本：fix_security_issues.py

修复内容：
1. ✓ SQL注入 → 使用参数化查询
2. ✓ XSS → 添加HTML转义
3. ✓ 硬编码密码 → 使用环境变量

运行修复？
```

## 质量标准

### 代码质量指标

| 指标 | 优秀 | 良好 | 合格 | 不合格 |
|------|------|------|------|--------|
| 代码覆盖率 | ≥90% | 80-90% | 70-80% | <70% |
| 代码复杂度 | ≤5 | 6-10 | 11-15 | >15 |
| 重复代码率 | ≤2% | 2-5% | 5-10% | >10% |
| 技术债务 | ≤1h | 1-4h | 4-8h | >8h |

### 安全标准

| 漏洞等级 | 数量要求 | 处理时限 |
|----------|----------|----------|
| 高危 | 0 | 立即修复 |
| 中危 | ≤2 | 7天内 |
| 低危 | ≤5 | 30天内 |
| 信息 | 不限 | 不强制 |

### 性能标准

| 指标 | 标准 |
|------|------|
| API响应时间 | P95 < 200ms |
| 数据库查询 | < 50ms |
| 内存使用 | < 512MB |
| CPU使用 | < 70% |

## 质量检查清单

### 代码规范

- [ ] 代码格式符合规范
- [ ] 命名清晰有意义
- [ ] 注释充分且准确
- [ ] 无硬编码配置
- [ ] 无魔法数字

### 静态分析

- [ ] 无严重代码异味
- [ ] 复杂度在合理范围
- [ ] 无重复代码
- [ ] 无潜在Bug
- [ ] 异常处理完整

### 安全检查

- [ ] 无SQL注入风险
- [ ] 无XSS风险
- [ ] 无CSRF风险
- [ ] 敏感数据已加密
- [ ] 依赖无已知漏洞

### 性能检查

- [ ] 无明显性能瓶颈
- [ ] 数据库查询优化
- [ ] 无内存泄漏
- [ ] 资源正确释放

## 相关资源

- [质量标准参考](./references/quality-standards.md)
- [安全检查清单](./references/security-checklist.md)
- [性能优化指南](./references/performance-optimization.md)

---

**版本**: 1.0.0  
**最后更新**: 2026-05-28
