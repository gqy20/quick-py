# Python Kit

[![Copier](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/copier-org/copier/master/img/badge/badge-grayscale-inverted-border-orange.json)](https://github.com/copier-org/copier)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)

> 现代Python 项目模板 - 基于 Copier 模板生成器

一个专业的 Python 项目脚手架模板，使用 [Copier](https://copier.readthedocs.io/) 生成规范化的 Python 项目。

## 特性

- 📦 **uv** - 极速包管理器（比 pip 快 10-100 倍）
- 🏗️ **src layout** - 标准项目结构
- ⚡ **ruff** - 统一代码检查和格式化
- ✅ **pytest** - 测试框架
- 📝 **rich** - 美观的日志输出
- 🪝 **pre-commit** - 提交前检查
- 🔄 **CI/CD** - GitHub/GitLab CI 配置
- 🚀 **FastAPI** - 可选的 Web 开发示例
- 🔄 **模板更新** - 支持从模板合并更新

## 快速开始

### 安装 Copier

```bash
pip install copier
# 或
uv pip install copier
```

### 创建项目

```bash
# 从 GitHub 创建
copier copy https://github.com/gqy22/py_kit my-project

# 从本地创建
copier copy path/to/py_kit my-project
```

Copier 会交互式询问以下信息：

| 变量 | 说明 | 默认值 |
|------|------|--------|
| `project_name` | 项目名称 | My Project |
| `author_name` | 作者名称 | Your Name |
| `python_version` | Python 版本 | 3.13 |
| `ci_provider` | CI/CD 提供商 | GitHub CI |
| `add_api` | 添加 FastAPI 示例 | true |
| `license` | 开源协议 | MIT |

## 生成的项目结构

```
my-project/
├── .github/workflows/     # GitHub CI（可选）
├── .gitlab-ci.yml         # GitLab CI（可选）
├── src/my_package/        # 源代码
├── tests/                 # 测试
├── docs/                  # 文档
├── scripts/               # 工具脚本
├── .pre-commit-config.yaml
├── pyproject.toml
└── README.md
```

## 模板更新

从模板创建项目后，可以合并模板更新：

```bash
cd my-project
copier update
```

Copier 会智能合并更新，保留你的自定义修改。

## 模板变量

### 项目信息
- `project_name` - 项目名称
- `project_slug` - 项目 slug（URL友好）
- `package_name` - Python 包名
- `description` - 项目描述
- `version` - 初始版本号

### 作者信息
- `author_name` - 作者名称
- `author_email` - 作者邮箱

### 配置选项
- `python_version` - Python 版本 (3.11/3.12/3.13)
- `license` - 开源协议 (MIT/BSD-3-Clause/ISC/Apache-2.0/GPL-3.0)
- `ci_provider` - CI/CD 提供商 (GitHub CI/GitLab CI/None)
- `add_api` - 添加 FastAPI 示例
- `add_cli` - 添加 CLI 示例
- `line_length` - 代码行长度限制

### 仓库配置
- `repository_provider` - 仓库提供商 URL
- `repository_username` - 仓库用户名

## 开发

查看 [CLAUDE.md](CLAUDE.md) 了解模板开发规范。

## 许可证

MIT

Copyright © 2024 Your Name
