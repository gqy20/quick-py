.PHONY: venv install check format test clean all help

venv:
	uv venv

install: venv
	.venv/bin/python -m uv pip install -e ".[dev]"

check:
	ruff check .

format:
	ruff format .

test:
	pytest

test-cov:
	pytest --cov=src/{{ package_name }}

clean:
	find . -type d -name __pycache__ -exec rm -rf {} + 2>/dev/null || true
	find . -type f -name "*.pyc" -delete 2>/dev/null || true
	rm -rf .coverage htmlcov/ dist/ build/ *.egg-info .venv

all: check test

help:
	@echo "常用命令:"
	@echo "  make venv      - 创建虚拟环境"
	@echo "  make install   - 创建虚拟环境并安装依赖"
	@echo "  make check     - 代码检查"
	@echo "  make format    - 格式化代码"
	@echo "  make test      - 运行测试"
	@echo "  make test-cov  - 测试 + 覆盖率"
	@echo "  make clean     - 清理缓存（包括虚拟环境）"
	@echo "  make all       - 检查 + 测试"
