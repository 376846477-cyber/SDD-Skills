---
name: harness-coding
description: Harness编码阶段Skill - 管理代码实现和单元测试编写。包含代码框架搭建、核心功能实现、代码规范、单元测试、代码评审。触发关键词：开始编码、实现功能、写代码、单元测试、代码规范、coding、TDD
---

# Harness编码阶段

## 阶段概述

编码阶段是将设计转化为可执行代码的关键阶段。通过规范化的编码流程和最佳实践，确保代码质量、可维护性和可测试性。本阶段采用测试驱动开发（TDD）和代码评审机制，从源头保证代码质量。

## 核心活动

### 1. 代码框架搭建

**目标**：搭建项目基础代码结构

**活动内容**：
- 项目目录结构创建
- 依赖管理配置
- 基础类和接口定义
- 配置文件管理
- 日志框架集成

**输出产物**：
- 项目骨架代码
- 构建配置文件
- 依赖清单文件

### 2. 核心功能实现

**目标**：实现核心业务逻辑

**活动内容**：
- 业务逻辑编码
- 接口实现
- 数据访问层实现
- 异常处理
- 日志记录

**输出产物**：
- 功能源代码
- 配置文件
- 技术文档

### 3. 单元测试编写

**目标**：编写高质量的单元测试

**活动内容**：
- 测试用例设计
- 测试代码编写
- Mock对象创建
- 测试数据准备
- 测试覆盖率分析

**输出产物**：
- 单元测试代码
- 测试数据文件
- 覆盖率报告

### 4. 代码评审

**目标**：通过评审提升代码质量

**活动内容**：
- 代码规范检查
- 逻辑审查
- 安全审查
- 性能审查
- 测试审查

**输出产物**：
- 评审记录
- 问题清单
- 改进建议

### 5. 设计一致性验证

**目标**：验证代码实现与设计文档的一致性

**活动内容**：
- 功能一致性检查
- 代码与设计对应检查
- 代码真实存在性检查
- 设计功能到代码行号映射
- 一致性报告生成

**输出产物**：
- 代码-设计一致性检查报告
- 功能映射清单
- 问题修复建议

## 编码流程

### TDD开发流程

```
1. 🔴 红灯 - 编写失败的测试
   └─ 理解需求，编写测试用例

2. 🟢 绿灯 - 实现最小代码
   └─ 编写刚好能通过测试的代码

3. 🔄 重构 - 优化代码质量
   └─ 在测试保护下优化代码

4. ✅ 提交 - 完成功能开发
   └─ 提交代码，进入评审
```

### 标准编码流程

```
需求理解
    ↓
测试设计
    ├─ 正常场景测试
    ├─ 边界条件测试
    └─ 异常场景测试
    ↓
代码实现
    ├─ 接口实现
    ├─ 业务逻辑
    └─ 错误处理
    ↓
单元测试
    ├─ 执行测试
    └─ 覆盖率检查
    ↓
代码评审
    ├─ 自我评审
    └─ 同行评审
    ↓
设计一致性验证
    ├─ 功能一致性检查
    ├─ 代码与设计对应
    ├─ 代码真实存在性检查
    └─ 生成映射报告
    ↓
代码提交
    └─ 提交到版本控制
```

## 使用示例

### 场景1：TDD开发

```
用户：用TDD方式实现用户登录功能

AI：[触发harness-coding]
采用测试驱动开发模式，开始实现用户登录功能：

🔴 第一步：编写失败的测试

创建测试文件：test_auth.py

```python
import pytest
from auth import AuthService

class TestAuthService:
    
    def test_login_success(self):
        """测试登录成功"""
        auth = AuthService()
        result = auth.login("user@example.com", "password123")
        
        assert result['success'] is True
        assert 'token' in result
        assert result['user']['email'] == "user@example.com"
    
    def test_login_invalid_password(self):
        """测试密码错误"""
        auth = AuthService()
        result = auth.login("user@example.com", "wrong_password")
        
        assert result['success'] is False
        assert result['error'] == "密码错误"
    
    def test_login_user_not_found(self):
        """测试用户不存在"""
        auth = AuthService()
        result = auth.login("nonexistent@example.com", "password")
        
        assert result['success'] is False
        assert result['error'] == "用户不存在"
```

运行测试：失败 ❌（预期的红灯）

---

🟢 第二步：实现最小代码

创建实现文件：auth.py

```python
import hashlib
from datetime import datetime, timedelta
from typing import Dict, Optional

class AuthService:
    
    def __init__(self):
        self.users = {}  # 示例：内存存储
        self.sessions = {}
    
    def login(self, email: str, password: str) -> Dict:
        """用户登录"""
        
        # 查找用户
        if email not in self.users:
            return {
                'success': False,
                'error': '用户不存在'
            }
        
        # 验证密码
        user = self.users[email]
        if not self._verify_password(password, user['password_hash']):
            return {
                'success': False,
                'error': '密码错误'
            }
        
        # 生成token
        token = self._generate_token(email)
        
        return {
            'success': True,
            'token': token,
            'user': {
                'email': email,
                'name': user['name']
            }
        }
    
    def _verify_password(self, password: str, password_hash: str) -> bool:
        """验证密码"""
        return hashlib.sha256(password.encode()).hexdigest() == password_hash
    
    def _generate_token(self, email: str) -> str:
        """生成令牌"""
        return hashlib.sha256(
            f"{email}:{datetime.now().isoformat()}".encode()
        ).hexdigest()
```

运行测试：通过 ✅（绿灯）

---

🔄 第三步：重构优化

优化点识别：
1. 密码哈希算法应使用bcrypt
2. Token应使用JWT
3. 用户存储应抽象为数据访问层

重构代码：

```python
import bcrypt
import jwt
from datetime import datetime, timedelta
from typing import Dict, Optional
from user_repository import UserRepository

class AuthService:
    
    def __init__(self, user_repo: UserRepository):
        self.user_repo = user_repo
        self.secret_key = "your-secret-key"
        self.token_expire_hours = 24
    
    def login(self, email: str, password: str) -> Dict:
        """用户登录"""
        
        # 查找用户
        user = self.user_repo.find_by_email(email)
        if not user:
            return {
                'success': False,
                'error': '用户不存在'
            }
        
        # 验证密码
        if not self._verify_password(password, user.password_hash):
            return {
                'success': False,
                'error': '密码错误'
            }
        
        # 生成JWT token
        token = self._generate_jwt_token(user)
        
        return {
            'success': True,
            'token': token,
            'user': {
                'id': user.id,
                'email': user.email,
                'name': user.name
            }
        }
    
    def _verify_password(self, password: str, password_hash: str) -> bool:
        """验证密码（使用bcrypt）"""
        return bcrypt.checkpw(
            password.encode('utf-8'),
            password_hash.encode('utf-8')
        )
    
    def _generate_jwt_token(self, user) -> str:
        """生成JWT令牌"""
        payload = {
            'user_id': user.id,
            'email': user.email,
            'exp': datetime.utcnow() + timedelta(hours=self.token_expire_hours)
        }
        return jwt.encode(payload, self.secret_key, algorithm='HS256')
```

运行测试：通过 ✅

---

📊 测试覆盖率报告

文件：auth.py
覆盖率：95%

未覆盖代码：
- 异常处理分支：3行
- 日志记录：5行

建议：添加异常场景测试

---

✅ 第四步：代码评审

自动评审结果：

✓ 代码规范：通过
✓ 类型提示：完整
✓ 文档字符串：完整
✓ 异常处理：合理

改进建议：
1. secret_key应从配置读取
2. 添加登录失败次数限制
3. 添加日志记录

是否提交代码进行同行评审？
```

### 场景2：代码框架搭建

```
用户：搭建Flask项目框架

AI：正在创建Flask项目框架...

📁 项目目录结构

```
my_flask_app/
├── app/
│   ├── __init__.py          # 应用工厂
│   ├── config.py             # 配置管理
│   ├── models/               # 数据模型
│   │   ├── __init__.py
│   │   └── user.py
│   ├── routes/               # 路由
│   │   ├── __init__.py
│   │   └── auth.py
│   ├── services/             # 业务逻辑
│   │   ├── __init__.py
│   │   └── auth_service.py
│   ├── utils/                # 工具函数
│   │   ├── __init__.py
│   │   └── decorators.py
│   └── extensions.py         # 扩展初始化
├── tests/                    # 测试
│   ├── __init__.py
│   ├── conftest.py
│   ├── test_auth.py
│   └── test_models/
├── migrations/               # 数据库迁移
├── requirements.txt          # 依赖清单
├── config.py                 # 配置文件
├── .env.example              # 环境变量示例
├── .gitignore               # Git忽略文件
├── README.md                 # 项目文档
└── run.py                    # 启动文件
```

创建关键文件...

📄 requirements.txt

```
Flask==3.0.0
Flask-SQLAlchemy==3.1.1
Flask-Migrate==4.0.5
Flask-JWT-Extended==4.6.0
bcrypt==4.1.2
python-dotenv==1.0.0
pytest==7.4.3
pytest-cov==4.1.0
```

📄 app/__init__.py

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate
from flask_jwt_extended import JWTManager

db = SQLAlchemy()
migrate = Migrate()
jwt = JWTManager()

def create_app(config_name='default'):
    """应用工厂函数"""
    app = Flask(__name__)
    
    # 加载配置
    from app.config import config
    app.config.from_object(config[config_name])
    
    # 初始化扩展
    db.init_app(app)
    migrate.init_app(app, db)
    jwt.init_app(app)
    
    # 注册蓝图
    from app.routes.auth import auth_bp
    app.register_blueprint(auth_bp, url_prefix='/api/v1/auth')
    
    return app
```

📄 config.py

```python
import os
from dotenv import load_dotenv

load_dotenv()

class Config:
    SECRET_KEY = os.environ.get('SECRET_KEY') or 'dev-secret-key'
    SQLALCHEMY_DATABASE_URI = os.environ.get('DATABASE_URL') or \
        'postgresql://localhost/myapp'
    SQLALCHEMY_TRACK_MODIFICATIONS = False
    JWT_SECRET_KEY = os.environ.get('JWT_SECRET_KEY') or 'jwt-secret-key'
    JWT_ACCESS_TOKEN_EXPIRES = 3600  # 1 hour

class DevelopmentConfig(Config):
    DEBUG = True

class ProductionConfig(Config):
    DEBUG = False

config = {
    'development': DevelopmentConfig,
    'production': ProductionConfig,
    'default': DevelopmentConfig
}
```

📄 run.py

```python
from app import create_app

app = create_app(os.getenv('FLASK_ENV') or 'default')

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

---

✅ 项目框架搭建完成！

下一步建议：
1. 配置数据库连接
2. 创建数据模型
3. 实现业务逻辑
```

### 场景3：代码评审

```
用户：评审这段代码

[代码片段]
```python
def process_order(order_id):
    order = get_order(order_id)
    if order.status == 'pending':
        order.status = 'processing'
        save_order(order)
        send_email(order.user.email, "订单处理中")
        return True
    return False
```

AI：正在评审代码...

📊 代码评审报告

**代码规范检查** ✓

- 命名规范：符合PEP8
- 代码格式：符合要求
- 类型提示：缺失

**逻辑审查** ⚠

问题：
1. 缺少异常处理
2. 缺少事务管理
3. 缺少日志记录
4. 硬编码字符串

风险：
- save_order失败后，状态可能不一致
- send_email失败会导致订单处理失败

**安全审查** ⚠

问题：
1. 缺少权限验证
2. 没有防重放机制

**性能审查** ⚠

问题：
1. 同步发送邮件可能阻塞
2. 缺少缓存机制

---

💡 改进建议

```python
from typing import Optional
import logging
from functools import wraps

logger = logging.getLogger(__name__)

def process_order(order_id: int) -> bool:
    """处理订单
    
    Args:
        order_id: 订单ID
        
    Returns:
        bool: 处理成功返回True，否则返回False
        
    Raises:
        OrderNotFoundError: 订单不存在
        PermissionError: 无权限操作
    """
    try:
        # 权限验证
        if not has_permission(current_user, 'process_order'):
            raise PermissionError("无权限处理订单")
        
        # 获取订单
        order = get_order(order_id)
        if not order:
            logger.warning(f"订单不存在: {order_id}")
            return False
        
        # 状态检查
        if order.status != OrderStatus.PENDING:
            logger.info(f"订单状态不允许处理: {order_id}, {order.status}")
            return False
        
        # 使用事务更新订单状态
        with db.transaction():
            order.status = OrderStatus.PROCESSING
            order.updated_at = datetime.now()
            save_order(order)
            
            # 异步发送通知
            send_email_async(
                to=order.user.email,
                subject="订单处理中",
                template="order_processing",
                data={'order': order}
            )
            
            logger.info(f"订单处理成功: {order_id}")
            return True
            
    except Exception as e:
        logger.error(f"处理订单失败: {order_id}, 错误: {str(e)}")
        raise
```

改进点：
1. ✓ 添加类型提示和文档字符串
2. ✓ 添加异常处理和日志记录
3. ✓ 使用事务保证一致性
4. ✓ 异步发送邮件避免阻塞
5. ✓ 权限验证
6. ✓ 使用枚举替代魔法字符串

是否应用改进建议？
```

## 代码规范

### 命名规范

| 类型 | 规范 | 示例 |
|------|------|------|
| 类名 | 大驼峰 | `UserService` |
| 函数名 | 小写下划线 | `get_user_by_id` |
| 变量名 | 小写下划线 | `user_count` |
| 常量 | 大写下划线 | `MAX_RETRY_COUNT` |
| 私有方法 | 单下划线前缀 | `_validate_input` |

### 注释规范

```python
def calculate_discount(price: float, discount_rate: float) -> float:
    """计算折扣价格
    
    Args:
        price: 原价
        discount_rate: 折扣率（0-1之间）
        
    Returns:
        float: 折扣后的价格
        
    Raises:
        ValueError: 当discount_rate不在0-1范围内
        
    Example:
        >>> calculate_discount(100.0, 0.2)
        80.0
    """
    if not 0 <= discount_rate <= 1:
        raise ValueError("discount_rate must be between 0 and 1")
    
    return price * (1 - discount_rate)
```

### 类型提示

```python
from typing import List, Dict, Optional, Union

def get_users(
    age: Optional[int] = None,
    status: str = 'active'
) -> List[Dict[str, Union[str, int]]]:
    """获取用户列表"""
    pass
```

## 单元测试规范

### 测试命名

```python
class TestUserService:
    """用户服务测试"""
    
    def test_create_user_success(self):
        """测试创建用户成功"""
        pass
    
    def test_create_user_with_invalid_email(self):
        """测试使用无效邮箱创建用户"""
        pass
    
    def test_create_user_with_duplicate_email(self):
        """测试使用重复邮箱创建用户"""
        pass
```

### 测试结构

```python
def test_user_login():
    # Arrange - 准备测试数据
    user = create_test_user(email="test@example.com")
    
    # Act - 执行被测代码
    result = auth_service.login("test@example.com", "password")
    
    # Assert - 验证结果
    assert result['success'] is True
    assert 'token' in result
    
    # Cleanup - 清理测试数据
    delete_test_user(user.id)
```

### 测试覆盖场景

1. **正常场景**：正常输入，预期输出
2. **边界条件**：空值、最大值、最小值
3. **异常场景**：错误输入、异常情况
4. **并发场景**：多线程、并发访问

## 代码评审清单

### 功能正确性

- [ ] 代码是否实现了需求
- [ ] 是否处理了所有边界情况
- [ ] 错误处理是否完整
- [ ] 是否有潜在的bug

### 代码质量

- [ ] 代码是否易于理解
- [ ] 命名是否清晰
- [ ] 是否有重复代码
- [ ] 函数是否过长
- [ ] 是否有足够的注释

### 性能

- [ ] 是否有性能问题
- [ ] 是否有不必要的循环
- [ ] 是否有内存泄漏风险
- [ ] 数据库查询是否高效

### 安全

- [ ] 是否有权限验证
- [ ] 输入是否经过验证
- [ ] 敏感数据是否加密
- [ ] 是否有SQL注入风险

### 测试

- [ ] 单元测试是否充分
- [ ] 测试覆盖率是否达标
- [ ] 是否测试了异常场景

## 设计一致性验证

### 验证流程

```
1. 文档解析
   ├─ 读取设计文档(design.md)
   ├─ 读取PRD文档(prd.md)
   └─ 提取基准信息(模块、接口、数据模型)

2. 代码库扫描
   ├─ 使用glob扫描源代码文件
   ├─ 使用grep搜索关键代码模式
   └─ 使用read读取关键文件内容

3. 功能一致性检查
   ├─ 对比设计功能与代码实现
   ├─ 验证功能行为逻辑
   └─ 检查输入输出一致性

4. 代码与设计对应
   ├─ 模块对应检查
   ├─ 接口对应检查
   ├─ 数据模型对应检查
   └─ 配置项对应检查

5. 代码真实存在性
   ├─ 文件存在性验证
   ├─ 函数/方法存在性验证
   └─ 空实现检查

6. 生成报告
   ├─ 一致性评分
   ├─ 问题清单
   └─ 修复建议
```

### 验证检查项

#### 功能一致性检查

| 检查项 | 说明 | 状态 |
|-------|------|------|
| 功能完整性 | 设计中的所有功能是否都已实现 | ✓/✗ |
| 行为一致性 | 功能行为是否与设计描述一致 | ✓/✗ |
| 输入输出匹配 | 参数和返回值是否与设计一致 | ✓/✗ |
| 异常处理 | 边界条件和异常是否按设计处理 | ✓/✗ |

#### 代码与设计对应检查

**模块对应表**:

| 设计模块 | 代码位置 | 对应状态 | 差异说明 |
|---------|---------|---------|---------|
| 模块名称 | 文件路径 | ✓/部分/✗ | 说明 |

**接口对应表**:

| 设计接口 | 代码位置 | 方法一致 | 请求格式 | 响应格式 | 状态 |
|---------|---------|---------|---------|---------|------|
| API路径 | 文件:行号 | ✓/✗ | ✓/✗ | ✓/✗ | ✓/✗ |

**数据模型对应表**:

| 设计模型 | 代码位置 | 字段一致 | 类型一致 | 状态 |
|---------|---------|---------|---------|------|
| 模型名 | 文件:行号 | Y/N字段数 | Y/N类型数 | ✓/✗ |

#### 代码真实存在性检查

| 检查类型 | 检查项 | 状态 |
|---------|-------|------|
| 文件存在性 | 设计中提到的文件是否存在 | ✓/✗ |
| 函数存在性 | 设计中定义的函数是否存在 | ✓/✗ |
| 非空实现 | 函数是否有实际实现(非TODO/pass) | ✓/✗ |
| 依赖存在 | import的模块是否已安装 | ✓/✗ |

### 一致性报告模板

```markdown
# 代码-设计一致性检查报告

## 1. 检查概述

- 检查时间：YYYY-MM-DD HH:mm
- 设计文档：docs/design.md
- 代码范围：src/
- 扫描文件数：N个

## 2. 总体一致性评分

| 检查维度 | 一致率 | 评级 |
|---------|-------|------|
| 功能一致性 | X/Y (Z%) | 一致/基本一致/不一致 |
| 模块对应性 | X/Y (Z%) | 一致/基本一致/不一致 |
| 接口对应性 | X/Y (Z%) | 一致/基本一致/不一致 |
| 数据模型对应性 | X/Y (Z%) | 一致/基本一致/不一致 |
| 代码真实存在性 | X/Y (Z%) | 全部存在/部分缺失 |
| **综合评级** | | **通过/有条件通过/不通过** |

## 3. 功能一致性详情

| 设计功能 | 代码实现位置 | 状态 | 差异说明 |
|---------|------------|------|---------|
| 功能名称 | 文件:行号 | ✓/✗ | 说明 |

## 4. 模块对应详情

| 设计模块 | 代码位置 | 状态 | 差异 |
|---------|---------|------|------|
| 模块名 | 文件路径 | ✓/✗ | 说明 |

## 5. 接口对应详情

| 设计接口 | 代码位置 | 请求 | 响应 | 状态 |
|---------|---------|-----|------|------|
| API路径 | 文件:行号 | ✓/✗ | ✓/✗ | ✓/✗ |

## 6. 问题汇总

### 阻断性问题

| 编号 | 问题 | 修复建议 |
|-----|------|---------|
| ID | 问题描述 | 建议内容 |

### 一般问题

| 编号 | 问题 | 修复建议 |
|-----|------|---------|
| ID | 问题描述 | 建议内容 |
```

### 使用示例

#### 场景：编码完成后的设计一致性验证

```
AI：编码阶段已完成，开始设计一致性验证...

━━━━━━━━━━━━━━━━━━━━━

📋 阶段1：文档解析

读取设计文档：docs/design.md
读取PRD文档：docs/prd.md

提取基准信息：
- 功能模块：5个
- API接口：12个
- 数据模型：3个
- 配置项：8个

━━━━━━━━━━━━━━━━━━━━━

🔍 阶段2：代码库扫描

扫描源代码目录：src/
发现文件：23个

关键代码模式搜索：
- 路由定义：12个
- 数据模型：3个
- 服务类：8个

━━━━━━━━━━━━━━━━━━━━━

✓ 阶段3：功能一致性检查

功能模块一致性：
┌──────────────┬─────────────────┬──────┐
│ 设计模块      │ 代码实现         │ 状态 │
├──────────────┼─────────────────┼──────┤
│ 用户管理      │ src/user/       │ ✓    │
│ 权限管理      │ src/permission/ │ ✓    │
│ 订单管理      │ src/order/      │ ✓    │
│ 支付管理      │ src/payment/    │ ✓    │
│ 通知管理      │ src/notification/│ ✓   │
└──────────────┴─────────────────┴──────┘

一致率：5/5 (100%)

━━━━━━━━━━━━━━━━━━━━━

🔌 阶段4：接口对应检查

API接口对应：
┌────────────────────┬──────────────────┬────────┐
│ 设计接口            │ 代码位置          │ 状态   │
├────────────────────┼──────────────────┼────────┤
│ POST /api/users    │ src/routes/user.py:15 │ ✓ │
│ GET /api/users/{id}│ src/routes/user.py:28 │ ✓ │
│ PUT /api/users/{id}│ src/routes/user.py:42 │ ✓ │
│ POST /api/orders   │ src/routes/order.py:18│ ✓ │
│ GET /api/orders/{id}│src/routes/order.py:35│ ✓ │
└────────────────────┴──────────────────┴────────┘

一致率：12/12 (100%)

━━━━━━━━━━━━━━━━━━━━━

💾 阶段5：数据模型检查

数据模型对应：
┌────────┬───────────────────┬─────────┬─────────┐
│ 模型    │ 代码位置           │ 字段一致 │ 状态    │
├────────┼───────────────────┼─────────┼─────────┤
│ User   │ src/models/user.py│ 10/10   │ ✓      │
│ Order  │ src/models/order.py│ 15/15  │ ✓      │
│ Payment│ src/models/payment.py│ 8/8  │ ✓      │
└────────┴───────────────────┴─────────┴─────────┘

一致率：3/3 (100%)

━━━━━━━━━━━━━━━━━━━━━

🔎 阶段6：代码真实存在性检查

文件存在性：
✓ src/services/user_service.py
✓ src/services/order_service.py
✓ src/services/payment_service.py
✓ src/middleware/auth.py

函数存在性：
✓ UserService.create() - user_service.py:25
✓ UserService.get_by_id() - user_service.py:42
✓ OrderService.create() - order_service.py:18

空实现检查：
✗ payment_service.py:89 - process_refund() 只有TODO注释

━━━━━━━━━━━━━━━━━━━━━

📊 一致性检查报告

总体评分：95/100

评级：✓ 有条件通过

问题统计：
- 阻断性问题：0个
- 一般问题：1个
- 改进建议：3个

问题详情：
1. payment_service.py:89 - process_refund()为空实现
   建议：补充退款处理逻辑

改进建议：
1. 增加单元测试覆盖率
2. 补充API文档注释
3. 优化异常处理

报告已生成：reports/code-design-consistency-report.md

━━━━━━━━━━━━━━━━━━━━━

是否需要修复发现的问题？
```

### 一致性判定标准

#### 功能一致性评级

| 评级 | 一致率 | 说明 |
|-----|-------|------|
| 一致 | ≥90% | 功能完全实现且符合设计 |
| 基本一致 | 70-89% | 核心功能实现，存在非关键差异 |
| 不一致 | <70% | 功能缺失或严重偏离设计 |

#### 综合评级规则

- **通过**：所有维度一致率≥90%
- **有条件通过**：存在维度一致率70-89%
- **不通过**：任一维度一致率<70%

## 相关资源

- [代码规范指南](./references/coding-standards.md)
- [单元测试最佳实践](./references/unit-testing-guide.md)
- [代码评审指南](./references/code-review-guide.md)
- [设计一致性验证指南](./references/design-consistency-guide.md)

---

**版本**: 1.1.0  
**最后更新**: 2026-05-29
