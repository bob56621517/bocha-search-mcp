# AGENTS.md

## 项目概览

博查搜索 MCP Server — 基于 FastMCP (mcp 1.x) 的搜索服务，提供 `bocha_web_search` 和 `bocha_ai_search` 两个工具。

- **源码入口**: `src/bocha_search_mcp/__init__.py` 的 `main()` 函数
- **MCP Server 定义**: `src/bocha_search_mcp/server.py`
- **运行方式**: `uv run bob56621517-bocha-search-mcp`

## 关键约束

- **mcp 版本锁定**: `mcp[cli]>=1.6.0,<2.0.0`。绝对不能升到 2.0，FastMCP 在 2.0 中已移除。
- **FastMCP 构造函数**: 1.x 使用 `instructions` 参数（不是 `prompt`），不要改回去。
- **环境变量**: 必须设置 `BOCHA_API_KEY`，从 https://open.bochaai.com 获取。

## 项目名不一致

| 位置 | 名称 |
|---|---|
| PyPI 项目名 (`pyproject.toml`) | `bob56621517-bocha-search-mcp` |
| PyPI 入口脚本 | `bob56621517-bocha-search-mcp` |
| FastMCP server 名 (`server.py:16`) | `bocha-search-mcp` |
| 包目录名 | `bocha_search_mcp` |
| 用户安装命令 | `uvx bob56621517-bocha-search-mcp` |

## 常用命令

```bash
uv run bob56621517-bocha-search-mcp   # 本地运行
uv build                               # 构建分发包
npx @modelcontextprotocol/inspector uv run bob56621517-bocha-search-mcp  # MCP Inspector 调试
```

## 发版流程

1. 修改 `pyproject.toml` 中的 `version`
2. 提交并推送到 `master`（默认分支是 `master`，不是 `main`）
3. 打版本标签并推送: `git tag vX.Y.Z && git push origin vX.Y.Z`
4. GitHub Actions 自动构建并发布到 PyPI

## 技术细节

- **Python**: 3.12（见 `.python-version`）
- **构建**: `hatchling` + `uv`，src-layout
- **无测试**、无 lint/formatter 配置
- **CI**: 仅 `.github/workflows/publish.yml`（构建 + PyPI 发布）
