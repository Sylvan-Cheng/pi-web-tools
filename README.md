# pi-web-tools

pi coding agent 网页工具集 — Firecrawl + Tavily 双平台扩展 + 智能路由 skill。

## 工具概览

| 扩展 | 工具 | 功能 |
|------|------|------|
| **firecrawl** | `firecrawl_scrape` | 抓取单页（支持截图、JSON 提取、品牌分析、问答） |
| | `firecrawl_search` | 搜索 + 全文 markdown 一步获取 |
| | `firecrawl_crawl` | 异步整站爬取（异步轮询、路径过滤、sitemap） |
| | `firecrawl_map` | 发现站点 URL（含标题 + 描述） |
| | `firecrawl_usage` | 查询 credit 余额 |
| **tavily** | `tavily_search` | AI 优化搜索（含 LLM 生成答案） |
| | `tavily_extract` | 批量提取页面内容（最多 20 个 URL） |
| | `tavily_crawl` | 同步网站爬取（即发即回，150s 超时） |
| | `tavily_map` | 发现站点 URL 列表 |
| | `tavily_research` | 深度多源研究（生成含引用报告） |
| | `tavily_usage` | 查询 API 使用量与限额 |
| **skill** | `tool-routing` | 自动引导模型在 Tavily/Firecrawl 间选最优工具 |

## 安装

### 方式一：克隆安装

```bash
# 克隆主仓库（含子模块）
git clone --recurse-submodules https://github.com/Sylvan-Cheng/pi-web-tools.git
cd pi-web-tools

# 复制到 pi 扩展目录
cp -r .pi/extensions/* ~/.pi/agent/extensions/
cp -r .pi/skills/* ~/.pi/agent/skills/
```

### 方式二：单独安装某个扩展

```bash
# 仅安装 Firecrawl
git clone https://github.com/Sylvan-Cheng/pi-firecrawl-extension.git ~/.pi/agent/extensions/firecrawl

# 仅安装 Tavily
git clone https://github.com/Sylvan-Cheng/pi-tavily-extension.git ~/.pi/agent/extensions/tavily

# 仅安装 tool-routing skill
git clone https://github.com/Sylvan-Cheng/pi-web-tools.git /tmp/pi-web-tools
cp -r /tmp/pi-web-tools/.pi/skills/tool-routing ~/.pi/agent/skills/
```

### 方式三：开发模式（符号链接）

```bash
# 在 pi 扩展目录创建符号链接，修改后 /reload 即可生效
ln -s "$(pwd)/.pi/extensions/firecrawl" ~/.pi/agent/extensions/firecrawl
ln -s "$(pwd)/.pi/extensions/tavily" ~/.pi/agent/extensions/tavily
ln -s "$(pwd)/.pi/skills/tool-routing" ~/.pi/agent/skills/tool-routing
```

Windows 用户用管理员 PowerShell 执行：
```powershell
New-Item -ItemType Junction -Path "$env:USERPROFILE\.pi\agent\extensions\firecrawl" -Target "D:\Codes\vibecoding\plugins\.pi\extensions\firecrawl"
New-Item -ItemType Junction -Path "$env:USERPROFILE\.pi\agent\extensions\tavily" -Target "D:\Codes\vibecoding\plugins\.pi\extensions\tavily"
New-Item -ItemType Junction -Path "$env:USERPROFILE\.pi\agent\skills\tool-routing" -Target "D:\Codes\vibecoding\plugins\.pi\skills\tool-routing"
```

## 配置 API Key

```bash
# 获取 API Key
# Firecrawl: https://www.firecrawl.dev/app/api-keys
# Tavily:     https://app.tavily.com

# 方式一：写入 ~/.bashrc 或 ~/.bash_profile（推荐）
echo 'export FIRECRAWL_API_KEY="fc-..."' >> ~/.bashrc
echo 'export TAVILY_API_KEY="tvly-..."' >> ~/.bashrc
source ~/.bashrc

# 方式二：Windows 系统环境变量
# 控制面板 → 系统 → 高级系统设置 → 环境变量 → 用户变量 → 新建
# 变量名: FIRECRAWL_API_KEY / TAVILY_API_KEY
```

## 使用

安装后重启 pi（或 `/reload`），11 个工具自动注册。模型会根据 `tool-routing` skill 自动选择最合适的工具。

```bash
# 启动 pi
pi
```

## 项目结构

```
pi-web-tools/
├── .pi/
│   ├── extensions/
│   │   ├── firecrawl/          # [submodule] Firecrawl 扩展
│   │   │   ├── client.ts       #   HTTP 客户端
│   │   │   ├── index.ts        #   5 个工具注册
│   │   │   └── types.ts        #   Firecrawl v2 API 类型
│   │   └── tavily/             # [submodule] Tavily 扩展
│   │       ├── client.ts       #   HTTP 客户端
│   │       ├── index.ts        #   6 个工具注册
│   │       └── types.ts        #   Tavily API 类型
│   └── skills/
│       └── tool-routing/
│           └── SKILL.md        # 工具选择决策指南
├── .gitmodules
├── .gitignore
└── README.md
```

## 更新

```bash
# 更新主仓库和子模块到最新
git pull --recurse-submodules
git submodule update --remote

# 重新复制到 pi
cp -r .pi/extensions/* ~/.pi/agent/extensions/
cp -r .pi/skills/* ~/.pi/agent/skills/
```
