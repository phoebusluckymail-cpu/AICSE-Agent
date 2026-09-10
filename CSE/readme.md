# CSE · 多 Agent 意识模拟程序 / Multi-Agent Consciousness Simulator

> AICSE 项目的工程实现部分。完整项目介绍、架构说明与设计思路请见[仓库根 README](../README.md)。
>
> *The engineering part of the AICSE project. See the [root README](../README.md) for the full project overview and architecture.*

---

## 使用须知 / Before You Start

1. **需要设置模型 API**：本项目基于 LLM Agent，必须配置 API Key。请在 `consciousness_sim/config.json` 中填写 `api.api_key`，或设置环境变量 `DEEPSEEK_API_KEY`。`base_url` 兼容 OpenAI 格式，可自行替换为其他模型服务。
2. **注意**：此为实验项目，其上下文管理机制与 AI 对话框内的模拟不同，实测效果不稳定，仅供研究和学习使用。
3. **建议**：若只是想体验「意识工程」的思路，建议直接使用 `../Prompt/` 中的提示词，交给一个专业级大模型即可，例如开启思考模式的 DeepSeek。

1. **API setup required**: this project runs on LLM agents and needs an API key. Fill in `api.api_key` in `consciousness_sim/config.json`, or set the `DEEPSEEK_API_KEY` environment variable. `base_url` speaks the OpenAI-compatible protocol, so you can swap in any other provider.
2. **Note**: this is an experimental project. Its context management differs from in-chat simulation and real-world results are unstable — research and learning use only.
3. **Suggestion**: to simply experience the idea behind this project, paste a prompt from `../Prompt/` into a capable LLM (thinking mode enabled) instead.

---

## 快速开始 / Quick Start

```bash
# 1. 安装依赖（仅 openai + streamlit）
pip install -r requirements.txt

# 2. 配置 API Key：编辑 consciousness_sim/config.json 的 api.api_key
#    或设置环境变量 DEEPSEEK_API_KEY

# 3. 运行
python run.py        # CLI 版（或双击 启动CLI版.bat）
python run_web.py    # Web 版（或双击 启动网页版.bat）→ http://localhost:8501
```

**CLI 指令**：输入任意问题即作为「种子」启动思考循环；`继续` 推进下一轮；`debug` 查看系统状态；`exit` 退出。

**CLI commands**: any question starts the loop as a *seed*; `继续` advances one round; `debug` prints system status; `exit` quits.

---

## 目录结构 / Layout

```
CSE/
├── run.py                  CLI 入口 / CLI entry point
├── run_web.py              Web 入口 / Web entry point
├── requirements.txt        openai + streamlit
├── 启动CLI版.bat / 启动网页版.bat
└── consciousness_sim/
    ├── app.py              Streamlit Web UI
    ├── main.py             CLI 主界面
    ├── engine.py           意识循环引擎 / consciousness loop engine
    ├── models.py           意识流数据结构 / stream data structures
    ├── agent_modules.py    6 发散模块 + 合成器 / 写入器 / 表达器
    ├── llm_client.py       LLM 通信层 / LLM transport
    ├── session_manager.py  会话持久化 / session persistence
    ├── prompt_loader.py    提示词加载 / prompt loader
    ├── config.py           配置读取 / config loading
    ├── config.json         API / 引擎 / 显示配置
    └── prompts/*.md        11 个 Agent 提示词，改 Markdown 即改行为
```

---

## 重要提示 / Important

- `config.json` 里的 `api_key` **不要提交到公开仓库**，请使用环境变量或本地文件。
- 每轮思考约产生 **9 次 LLM 调用**（6 个发散模块 + 合成器 + 意识流写入器 + 语言表达器），注意 API 成本。
- 会话数据保存在项目根目录的 `conversations/` 下，可用 Web 界面侧栏加载历史会话。

- **Never commit** the `api_key` in `config.json` to a public repository — use environment variables instead.
- Each thinking round costs roughly **9 LLM calls** (6 divergent modules + synthesizer + stream writer + expressor).
- Session data is stored under `conversations/`; load past sessions from the Web sidebar.
