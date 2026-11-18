# 📊 AI Data Analysis Agent（本地 Ollama 版）

基于 Agno Agent 框架 + **本地 Ollama 模型**（默认 `qwen2.5:7b`）的数据分析 Agent。上传 CSV / Excel 文件后，用自然语言提问，Agent 通过 DuckDB 生成 SQL 查询并返回结果，无需 OpenAI API Key。

## 与原版的区别

| 项目 | 原版 | 本版本 |
|---|---|---|
| 模型 | OpenAI `gpt-4o` | 本地 Ollama（`qwen2.5:7b`，可改） |
| 鉴权 | 需要 OpenAI API Key | 不需要 Key，连本机 Ollama |
| 依赖 | `openai` | `ollama` Python 包 |

## 功能

- 上传 CSV / Excel，自动识别数据类型与表结构
- 自然语言转 SQL（DuckDB），无需手写 SQL
- 聚合、筛选、排序、统计摘要
- Streamlit 交互界面

## 运行步骤

### 1. 安装并启动 Ollama

下载安装：https://ollama.com/download

启动本地服务（桌面应用会自动后台运行；命令行可执行 `ollama serve`），默认地址 `http://localhost:11434`。

### 2. 拉取模型

```bash
ollama pull qwen2.5:7b
# 内存偏小可换小模型：ollama pull qwen2.5:3b
```

### 3. 安装 Python 依赖

```bash
cd ai_data_analysis_agent_ollama
pip install -r requirements.txt
```

### 4. 启动应用

```bash
streamlit run ai_data_analyst.py
```

在网页侧边栏确认 Ollama 地址和模型名，上传 CSV / Excel 后即可提问。

## 可选：更换模型

- 直接在界面侧边栏的 `Model` 输入框填写已拉取的模型名；
- 或修改 `ai_data_analyst.py` 顶部的 `DEFAULT_OLLAMA_MODEL`。

## 注意事项

- 工具调用（function calling）的效果取决于本地模型能力；若模型不会调用 DuckDB/Pandas 工具，可换用工具调用支持更好的模型（如 `qwen2.5:14b`、`llama3.1:8b`）。
- 7B 模型建议内存 16 GB 以上；集显或内存不足时优先用 3B 量化版。
