# Repository Guidelines

## 项目结构与模块组织
`trendradar/` 为核心抓取与报告生成（crawler、report、notification、storage、utils）。`mcp_server/` 提供 MCP 服务端（services、tools、utils）。`config/` 存放 `config.yaml` 与 `frequency_words.txt`，运行必需。`output/` 为生成报告/快照，尽量避免在 PR 中新增。`docker/` 包含容器入口脚本与 `manage.py`。

## 构建、测试与本地运行
`./setup-mac.sh` 或 `setup-windows.bat` 安装 `uv` 并执行 `uv sync`。本地抓取：`uv run python -m trendradar`。MCP HTTP 模式：`./start-http.sh` 或 `start-http.bat`（等价于 `uv run python -m mcp_server.server --transport http --port 3333`）。请确保 `config/` 下配置文件存在。

## 编码风格与命名
Python 3.10+，4 空格缩进；模块/函数使用 snake_case，类使用 CamelCase，常量使用 UPPER_SNAKE。项目未配置统一格式化工具，请保持现有注释与类型标注风格。

## 测试指南
仓库未包含自动化测试目录。变更后至少运行主流程并检查 `output/` 生成内容；若改动 MCP 接口，可访问 `http://localhost:3333/mcp` 验证。若新增测试，建议放在 `tests/` 并使用 `pytest`。

## 提交与 PR
Git 历史仅有 `Initial commit`，尚无固定规范。建议提交信息使用简短祈使句并带范围，如 `crawler: handle timeout`。PR 需说明配置影响、运行方式与验证结果；若修改报告模板/HTML，请附示例截图或样例输出。

## 配置与安全
不要在仓库中提交真实 Token/Webhook。配置默认放在 `config/`，敏感项建议通过环境变量或私密配置覆盖，并在 PR 中标注。
