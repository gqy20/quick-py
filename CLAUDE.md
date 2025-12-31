# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

**Python Kit** 是一个 Python 标准项目模板，使用 [Copier](https://copier.readthedocs.io/) 生成规范化的 Python 项目。它不是一个可安装的包，而是一个可供复制和自定义的项目模板。

**关键特性：**
- 使用 `uv` 进行极快的包管理（比 pip 快 10-100 倍）
- 采用 src layout 标准项目结构
- 统一使用 ruff 进行代码检查和格式化
- 基于 Rich 的美观日志系统
- FastAPI Web 开发示例（可选）

## 模板开发（模板维护者）

如果你是模板维护者，需要修改模板本身：

```bash
# 在模板根目录工作
cd /path/to/py_kit

# 模板变量定义在 copier.yml
# 模板文件使用 Jinja2 语法，例如：
# {{ cookiecutter.package_name }} - Python 包名
# {{ cookiecutter.project_name }} - 项目名称
# {% if cookiecutter.add_api %}...{% endif %} - 条件块

# 测试模板生成
copier copy . /tmp/test-project

# 更新 .copier-answers.yml 默认值
```

## 用户使用（模板使用者）

### 创建新项目
```bash
# 使用模板创建项目
copier copy https://github.com/gqy22/py_kit my-project
cd my-project
```

### 环境设置
```bash
# 创建虚拟环境
uv venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate

# 安装项目及开发依赖
uv pip install -e ".[dev]"

# 安装 pre-commit 钩子
pre-commit install
```

### 代码质量检查
```bash
# 运行所有检查（推荐）
python scripts/check.py

# 单独运行各项检查
ruff check .              # 代码检查
ruff check --fix .        # 自动修复问题
ruff format .             # 格式化代码
ruff format --check .     # 检查格式
```

### 测试
```bash
pytest                           # 运行所有测试
pytest -v                        # 详细输出
pytest --cov=src/my_package --cov-report=html  # 覆盖率报告
pytest tests/test_core.py        # 运行特定文件
pytest tests/test_core.py::TestGreet::test_greet_default  # 特定测试
```

### FastAPI 开发（如果启用）
```bash
# 启动 API 服务器
python -m my_package.api

# 或使用 uvicorn
uvicorn my_package.api:app --reload
```

### 示例程序
```bash
python -m my_package.main    # 查看所有功能演示
```

## 代码架构

### 目录结构（生成后）
```
src/my_package/
├── __init__.py    # 包初始化，导出公共 API
├── core.py        # 基础功能演示（greet、add）
├── logger.py      # 日志管理系统（核心模块）
├── api.py         # FastAPI 应用示例（可选）
└── main.py        # 主程序入口
```

### 核心模块

**logger.py** - 日志系统
- 提供默认 `logger` 实例
- `get_logger(name)` - 获取或创建日志记录器
- `setup_logger(...)` - 自定义配置
- `console` - Rich 控制台用于直接输出
- 便捷函数：`print_success`、`print_error`、`print_warning`、`print_info`、`print_header`、`print_section`

**api.py** - FastAPI 应用（可选）
- 统一响应格式：`{"code": 0, "data": {}, "message": "成功"}`
- RESTful 风格路由：`/api/v1/` 前缀
- 完整的错误处理和日志记录
- 使用 `{% if cookiecutter.add_api %}` 条件块包含

### 导出公共 API
新增模块时，在 `src/my_package/__init__.py` 中导出需要公开的 API。

## 代码规范

1. **语言**：所有注释、文档字符串、日志消息使用**中文**
2. **命名**：函数和类使用英文命名（遵循 PEP 8）
3. **类型注解**：每个函数必须有类型注解
4. **文档字符串**：使用 Google 风格的中文文档字符串
5. **日志**：使用 `my_package.logger` 记录日志
6. **测试**：每个模块必须有对应的测试文件，目标覆盖率 >90%

## 模板变量

创建项目时，Copier 会询问以下变量（定义在 `copier.yml`）：

| 变量 | 说明 | 默认值 |
|------|------|--------|
| `project_name` | 项目名称 | My Project |
| `project_slug` | 项目 slug | 自动生成 |
| `package_name` | Python 包名 | 自动生成 |
| `author_name` | 作者名称 | Your Name |
| `author_email` | 作者邮箱 | your.email@example.com |
| `description` | 项目描述 | A short description |
| `version` | 初始版本 | 0.1.0 |
| `python_version` | Python 版本 | 3.13 |
| `license` | 开源协议 | MIT |
| `add_api` | 添加 FastAPI | true |
| `add_cli` | 添加 CLI | false |
| `line_length` | 代码行长度 | 88 |

## 模板开发规范

### 文件命名
- 源代码目录使用 `src/{{cookiecutter.package_name}}/`
- 测试文件使用 `tests/test_{{cookiecutter.package_name}}.py`

### Jinja2 语法
```python
# 变量替换
{{ cookiecutter.package_name }}

# 条件块
{% if cookiecutter.add_api -%}
from fastapi import FastAPI
{% endif %}

# 默认值处理
{{ cookiecutter.project_name | default("My Project") }}
```

### 避免硬编码
- 所有包名引用使用 `{{cookiecutter.package_name}}`
- 所有项目 slug 使用 `{{cookiecutter.project_slug}}`
- 日志文件名使用 `{{cookiecutter.project_slug}}.log`

## Pre-commit 钩子

项目使用 pre-commit 在提交前自动运行代码检查：
- trailing-whitespace - 删除行尾空格
- end-of-file-fixer - 确保文件以换行符结尾
- check-yaml/check-json/check-toml - 验证配置文件
- check-merge-conflict - 检测未解决的合并冲突
- ruff --fix - 自动修复代码问题
- ruff-format - 自动格式化代码

## 发布流程

```bash
# 1. 更新版本号（src/my_package/__init__.py 和 pyproject.toml）
# 2. 更新 docs/CHANGELOG.md
# 3. 创建并推送标签
git tag -a v0.2.0 -m "版本 0.2.0"
git push origin v0.2.0
# GitHub Actions 自动创建 Release 和发布到 PyPI
```

## 模板更新

从模板创建项目后，可以通过以下命令合并模板更新：

```bash
copier update
```

Copier 会智能合并更新，保留你的自定义修改。

## Git 提交规范

遵循简洁明了的提交规范，每次提交只做一件事。使用中文描述：
- `feat:` - 新功能
- `fix:` - 修复
- `docs:` - 文档
- `refactor:` - 重构
- `test:` - 测试
- `chore:` - 构建/工具
