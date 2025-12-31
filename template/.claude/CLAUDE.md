# {{ cookiecutter.project_name }} - Claude Code 指令

## 项目概述

- **Python 版本**: {{ cookiecutter.python_version }}+
- **包管理**: uv（极速包管理器）
- **项目结构**: src layout
- **代码规范**: ruff（检查 + 格式化）
- **测试框架**: pytest
- **日志系统**: rich

## 常用命令

```bash
# 安装依赖
uv pip install -e ".[dev]"

# 代码检查
ruff check .
ruff check --fix .

# 格式化
ruff format .

# 测试
pytest
pytest --cov=src/{{ cookiecutter.package_name }}

# 运行检查脚本
python scripts/check.py
```

## 代码规范

1. **语言**: 所有注释、文档字符串使用中文
2. **命名**: 函数和类使用英文（遵循 PEP 8）
3. **类型注解**: 必需
4. **文档字符串**: Google 风格中文文档
5. **提交规范**: feat/fix/docs/refactor/test/chore

{% if cookiecutter.add_api -%}
## API 开发

```bash
# 启动 FastAPI 服务器
python -m {{ cookiecutter.package_name }}.api

# 或使用 uvicorn
uvicorn {{ cookiecutter.package_name }}.api:app --reload
```
{% endif %}

## 项目结构

```
src/{{ cookiecutter.package_name }}/
├── __init__.py    # 包初始化，导出公共 API
├── core.py        # 核心功能
├── logger.py      # 日志系统
{% if cookiecutter.add_api -%}
├── api.py         # FastAPI 应用
{% endif %}
└── main.py        # 主程序入口
```
