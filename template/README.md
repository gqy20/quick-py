# {{ cookiecutter.project_name }}

{{ cookiecutter.description }}

[![CI](https://img.shields.io/badge/GitHub-Actions-blue)]({{ cookiecutter.repository_provider }}/{{ cookiecutter.repository_username }}/{{ cookiecutter.project_slug }}/actions)
[![Python {{ cookiecutter.python_version }}+](https://img.shields.io/badge/python-{{ cookiecutter.python_version }}+-blue.svg)](https://www.python.org/downloads/)
[![Ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)

## 概述

现代 Python 项目脚手架，使用 `uv` + `ruff` + `rich` 构建。

**核心特性：**
- 📦 **uv** - 极速包管理器
- 🏗️ **src layout** - 标准项目结构
- ⚡ **ruff** - 代码检查和格式化
- ✅ **pytest** - 测试框架
- 📝 **rich** - 美观的日志和终端输出
- 🪝 **pre-commit** - 提交前检查
- 🔄 **CI/CD** - GitHub Actions
{% if cookiecutter.add_api -%}
- 🚀 **FastAPI** - Web 开发示例
{% endif %}

## 快速开始

**前置要求：**
- Python {{ cookiecutter.python_version }}+
- [uv](https://github.com/astral-sh/uv)

```bash
# 创建虚拟环境
uv venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate

# 安装依赖
uv pip install -e ".[dev]"

# 安装 pre-commit 钩子
pre-commit install

# 运行检查
python scripts/check.py
```

## 项目结构

```
{{ cookiecutter.project_slug }}/
├── src/{{ cookiecutter.package_name }}/
│   ├── __init__.py
│   ├── core.py
│   ├── logger.py
{% if cookiecutter.add_api -%}
│   ├── api.py
{% endif %}
│   └── main.py
├── tests/
├── docs/
├── scripts/
└── pyproject.toml
```

## 常用命令

### 代码检查
```bash
ruff check .              # 代码检查
ruff format .             # 格式化
```

### 测试
```bash
pytest
pytest --cov=src/{{ cookiecutter.package_name }}
```

{% if cookiecutter.add_api -%}
### FastAPI 开发
```bash
python -m {{ cookiecutter.package_name }}.api
```
{% endif %}

## 代码规范

1. **语言**：注释和文档使用**中文**
2. **命名**：函数和类使用英文
3. **类型注解**：必需
4. **文档字符串**：Google 风格

## 许可证

{{ cookiecutter.license }}

Copyright © {{ cookiecutter.copyright_date }} {{ cookiecutter.author_name }}
