# Academic Research Skills for Claude Code

[![Version](https://img.shields.io/badge/version-v4.0.3-blue)](https://github.com/Imbad0202/academic-research-skills/releases/tag/v4.0.3)
[![License: CC BY-NC 4.0](https://img.shields.io/badge/license-CC%20BY--NC%204.0-lightgrey)](https://creativecommons.org/licenses/by-nc/4.0/)
[![Sponsor](https://img.shields.io/badge/sponsor-Buy%20Me%20a%20Coffee-orange?logo=buy-me-a-coffee)](https://buymeacoffee.com/crucify020v)

[English](README.md)

一套完整的学术研究 Claude Code 技能包，涵盖从研究到论文出版的全流程。

---

## 功能特色

- **Deep Research** — 13 个 Agent 组成的研究团队，支援苏格拉底引导 + 系统性文献回顾 / PRISMA
- **Academic Paper** — 12 个 Agent 的论文撰写团队，含 LaTeX 输出强化、视觉化、修订教练、引用格式转换
- **Academic Paper Reviewer** — 多视角同儕审查，0-100 品质量表（主编 + 3 位动態审查者 + 魔鬼代言人）
- **Academic Pipeline** — 10 阶段全流程调度器，含自适应 checkpoint、宣称验证、素材护照

### 完整 Pipeline

```
研究 → 撰写 → 诚信审查 → 审稿（5人）→ 苏格拉底指导
  → 修订 → 再审 → 再修订 → 最终诚信审查 → 定稿
```

**核心特点：**
1. 自适应 checkpoint（FULL / SLIM / MANDATORY）
2. 审稿前诚信验证 — 100% 引用、数據、宣称验证（Phase A-E）
3. 两阶段审查，含魔鬼代言人 + 0-100 品质量表
4. 审稿与修订之間的苏格拉底修订指导
5. 出版前最终诚信验证
6. 输出格式：MD + DOCX + LaTeX（APA 7.0 `apa7` class / IEEE / Chicago）→ tectonic 编译 PDF
7. Pipeline 完成后自动产出协作品质評估（6 维度 1-100 分）
8. 素材护照（Material Passport）支援中途进入流程的来源追踪
9. 跨 skill 模式顾问（14 种情境 + 使用者典型）

---

## 实际产出展示

查看完整 10 阶段 pipeline 的实际产出 — 包含**同儕审查报告、诚信验证报告、完稿论文**：

**[瀏覽所有 pipeline 产出 →](examples/showcase/)**

| 产出物 | 说明 |
|--------|------|
| [完稿论文（英文）](examples/showcase/full_paper_apa7.pdf) | APA 7.0 格式，LaTeX 编译 |
| [完稿论文（中文）](examples/showcase/full_paper_zh_apa7.pdf) | 中文版，APA 7.0 |
| [诚信报告 — 审稿前](examples/showcase/integrity_report_stage2.5.pdf) | Stage 2.5：抓出 15 个虚构引用 + 3 个统计错误 |
| [诚信报告 — 最终](examples/showcase/integrity_report_stage4.5.pdf) | Stage 4.5：确認零回归 |
| [同儕审查第一轮](examples/showcase/stage3_review_report.pdf) | 主编 + 3 审查者 + 魔鬼代言人 |
| [复审](examples/showcase/stage3prime_rereview_report.pdf) | 修订后验证审查 |
| [同儕审查第二轮](examples/showcase/stage3_review_report_r2.pdf) | 追踪审查 |
| [回覆审查意见](examples/showcase/response_to_reviewers_r2.pdf) | 逐点回覆 |
| [出版后稽核报告](examples/showcase/post_publication_audit_2026-03-09.md) | 独立全引用稽核：发现 21/68 篇问题，通过了 3 轮诚信审查仍漏网 |

---

## 效能说明

> **建议模型：Claude Opus 4.6**，搭配 **Max plan**（或同等的延伸思考设定）。
>
> 完整学术 pipeline（10 阶段）会消耗**大量 token** — 单次完整执行可能超过 200K 输入 + 100K 输出 token，视论文长度和修订轮数而定。请依预算斟酌使用。
>
> 单独使用个別 skill（如只用 `deep-research` 或 `academic-paper-reviewer`）的消耗明顯較少。

### 建议设定

为获得最佳使用体验，建议启用以下 Claude Code 功能：

| 设定 | 功能说明 | 启用方式 | 官方文件 |
|------|---------|---------|---------|
| **Agent Team** | 产生子代理（subagent）平行执行研究、撰写、审查 — 多 Agent pipeline 的核心机制 | 设定 `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`（研究预覽） | [Agent Teams](https://code.claude.com/docs/en/agent-teams) |
| **Ralph Loop** | 在长时間 pipeline 阶段保持 session 持续運作，讓 Claude 能自主执行而不会逾时中斷 | 使用 `/ralph-loop` 启动 | [Ralph Loop](https://claude.com/plugins/ralph-loop) |
| **Skip Permissions** | 跳过每次工具使用的确認提示，实现全 pipeline 不中斷的自主执行 | 启动时加上 `claude --dangerously-skip-permissions` | [Permissions](https://docs.anthropic.com/en/docs/claude-code/cli-reference) · [Advanced Usage](https://docs.anthropic.com/en/docs/claude-code/advanced) |

> **⚠️ Skip Permissions 注意事项**：此旗标会停用所有工具使用的确認对话框。请自行斟酌使用 — 在可信任的长时間 pipeline 中非常方便，但会移除手动审核的安全机制。仅在你确定接受 Claude 自动执行档案读写、shell 指令等操作时才启用。

---

## 前置需求

### 安裝 Claude Code

**建议：原生安裝程式**（不需要 Node.js，自动更新）：

```bash
# macOS / Linux
curl -fsSL https://claude.ai/install.sh | bash

# Windows（PowerShell）
irm https://claude.ai/install.ps1 | iex
```

<details>
<summary>替代方案：npm 安裝（已棄用）</summary>

需要 Node.js 18+。

```bash
npm install -g @anthropic-ai/claude-code
```

</details>

### 设定 API Key

你需要一个 Anthropic API key，请至 https://console.anthropic.com/ 取得。

```bash
# Claude Code 首次执行时会提示输入 API key
claude
```

或设定环境变数：

```bash
export ANTHROPIC_API_KEY=sk-ant-xxxxx
```

---

## 安裝方式

### 方法一：作为专案 Skills（推薦）

将此 repo clone 到专案的 `.claude/skills/` 目录：

```bash
# 切换到你的专案根目录
cd /path/to/your/project

# 建立 skills 目录（若不存在）
mkdir -p .claude/skills

# Clone skills
git clone https://github.com/Imbad0202/academic-research-skills.git .claude/skills/academic-research-skills
```

接著将 `.claude/CLAUDE.md` 的内容复制到你专案的 `.claude/CLAUDE.md`（若已有则合并）。

> **全域安裝：** 若希望所有专案都能使用这些 skills，可安裝到 `~/.claude/skills/`：
> ```bash
> mkdir -p ~/.claude/skills
> git clone https://github.com/Imbad0202/academic-research-skills.git ~/.claude/skills/academic-research-skills
> ```

### 方法二：作为独立专案

```bash
# Clone repo
git clone https://github.com/Imbad0202/academic-research-skills.git

# 进入专案
cd academic-research-skills

# 启动 Claude Code
claude
```

<details>
<summary><strong>沒有安裝 Git？</strong>直接下载 ZIP</summary>

1. 前往 https://github.com/Imbad0202/academic-research-skills
2. 点擊綠色 **Code** 按鈕 → **Download ZIP**
3. 解压縮到你想要的位置
4. 方法一：将解压后的资料夹移动到你专案内的 `.claude/skills/academic-research-skills`
5. 独立使用：在解压后的资料夹中开启终端機，执行 `claude`

</details>

### 方法三：Claude Cowork（桌面版）

在 [Claude Cowork](https://claude.com/product/cowork) 中使用这些 skills — Claude Desktop 的 AI 自主工作区。

**选项 A：资料夹存取（最快）**

1. 将此 repo clone 到本機：
   ```bash
   git clone https://github.com/Imbad0202/academic-research-skills.git ~/academic-research-skills
   ```
2. 开启 Claude Desktop → 点擊上方 **Cowork** 分页
3. 选择 clone 下来的 `academic-research-skills` 资料夹作为工作目录
4. Claude 会自动从 `SKILL.md` 偵测并载入 skills

**选项 B：作为专案 Skills**

若你已有 Cowork 专案资料夹：
```bash
cd /path/to/your/project
mkdir -p .claude/skills
git clone https://github.com/Imbad0202/academic-research-skills.git .claude/skills/academic-research-skills
```

Skills 会在对话相关时自动载入 — 例如说「帮我写论文」会触发 `academic-paper`。

**需求：**
- Claude Desktop（最新版本）且已启用 Cowork
- 付費方案（Pro、Max、Team 或 Enterprise）

### 方法四：上傳至 claude.ai

claude.ai 的 Project 功能可以载入这些 skills，不需要安裝 Claude Code。

**步驟：**

1. 从这个 repo 下载所有 `SKILL.md` 档案（共 4 个）：
   - `deep-research/SKILL.md`
   - `academic-paper/SKILL.md`
   - `academic-paper-reviewer/SKILL.md`
   - `academic-pipeline/SKILL.md`

2. 登入 [claude.ai](https://claude.ai)

3. 建立新 Project：
   - 点擊左側栏 **Projects** → **Create Project**
   - 命名为「Academic Research」（或任意名稱）

4. 上傳 SKILL.md 档案：
   - 进入 Project → 点擊 **Project Knowledge**（右側面板）
   - 点擊 **Add Content** → **Upload Files**
   - 上傳 4 个 `SKILL.md` 档案

5. （选用）上傳 reference 和 template 档案以获得更好效果：
   - `deep-research/references/` 下的档案（APA 指南、方法论模板等）
   - `academic-paper/references/` 下的档案（引用格式、写作风格等）
   - `academic-paper/templates/` 下的档案（论文结构模板）

6. 开始对话：在 Project 中开启新对话，直接说「引导我研究 X」或「帮我写论文」

**claude.ai 限制：**
- Project Knowledge 档案大小上限为每个档案 200KB
- SKILL.md 的 YAML frontmatter 中 `version` 和 `last_updated` 必须在 `metadata:` 下，否则上傳会失败
- claude.ai 不支援多 agent 平行执行，效果不如 Claude Code 完整
- 建议至少上傳 4 个 SKILL.md + 核心 references，以获得最佳效果

---

## 使用方式

### 快速开始

```
# 启动完整研究 pipeline
你: "我想做一篇关于 AI 对高教品保影響的研究论文"

# 苏格拉底引导模式
你: "引导我研究 AI 在教育評鑑中的应用"

# 引导式论文撰写
你: "引导我写一篇关于少子化影響的论文"

# 审查现有论文
你: "帮我审查这篇论文"（接著提供论文）

# 查看 pipeline 进度
你: "进度" 或 "status"
```

### 个別 Skill 使用

#### Deep Research（深度研究，7 种模式）
```
"研究 AI 对高等教育的影響"                    → full mode（完整研究）
"给我一份 X 的快速摘要"                       → quick mode（快速简报）
"帮我做 X 的系统性文献回顾，含 PRISMA"        → systematic-review mode（新增）
"引导我研究 X"                                → socratic mode（苏格拉底引导）
"帮我查核这些说法"                            → fact-check mode（事实查核）
"帮我做文献回顾"                              → lit-review mode（文献回顾）
"审查这篇论文的研究品质"                      → review mode（论文审查）
```

#### Academic Paper（学术论文撰写，9 种模式）
```
"帮我写一篇论文"                              → full mode（完整撰写）
"引导我写论文"                                → plan mode（引导规划）
"我有初稿，这是审稿意见"                      → revision mode（修订）
"帮我整理这些审稿意见成修订路线图"            → revision-coach mode（新增）
"转换成 LaTeX" / "引用格式转 IEEE"            → format-convert mode（格式转换）
"检查引用格式"                                → citation-check mode（引用检查）
"写一份中英双语摘要"                          → bilingual-abstract mode（双语摘要）
"潤飾我的写作风格"                            → writing-polish mode（写作潤飾）
"自动完成整篇论文"                            → full-auto mode（全自动撰写）
```

#### Academic Paper Reviewer（论文审查，5 种模式）
```
"审查这篇论文"                                → full mode（主编 + R1/R2/R3 + 魔鬼代言人）
"快速評估这篇论文"                            → quick mode（快速評估）
"引导我改进这篇论文"                          → guided mode（引导改进）
"检查研究方法"                                → methodology-focus mode（方法论聚焦）
"验收修订"                                    → re-review mode（再审验收）
```

#### Academic Pipeline（全流程调度器）
```
"我想做一篇完整的研究论文"                    → 从 Stage 1 开始完整 pipeline
"我已经有论文，帮我审查"                      → 从 Stage 2.5 进入（先做诚信审查）
"我收到审稿意见了"                            → 从 Stage 4 进入
```
> Pipeline 结束时自动产出 **Stage 6：过程紀录** — 含论文創建过程紀录与 6 维度协作品质評估（1–100 分）。

### 支援语言

- **简体中文** — 使用者以中文对话时预设使用
- **English** — 使用者以英文对话时预设使用
- 学术论文自动产出双语摘要（中文 + English）

> **使用其他语言？** 苏格拉底模式（deep-research）和 Plan 模式（academic-paper）採用**意图匹配**启动 — 偵测你的请求含義，而非比对特定关键字。这代表它們**支援任何语言**，無需額外设定。
>
> 不过，一般的 `Trigger Keywords` 区块（決定 skill 是否被启动）仍以英文和简体中文为主。如果你发现 skill 在你的语言下触发不穩定，可以在各 `SKILL.md` 的 `### Trigger Keywords` 区块中加入你的语言的关键字，提高匹配信心。

### 支援引用格式

- APA 7.0（预设，含中文引用规则）
- Chicago（Notes & Author-Date）
- MLA
- IEEE
- Vancouver

### 支援论文结构

- IMRaD（实证研究）
- 主题式文献回顾
- 理论分析
- 个案研究
- 政策简报
- 研讨会论文

---

## Skill 詳細资訊

### Deep Research (v2.3)

13 个 Agent 的严謹学术研究 pipeline：

| Agent | 角色 |
|-------|------|
| Research Question Agent | FINER 評分的研究问题制定 |
| Research Architect | 研究方法设计 |
| Bibliography Agent | 系统性文献搜索 |
| Source Verification Agent | 证據分级、掠奪性期刊偵测 |
| Synthesis Agent | 跨来源整合 |
| Report Compiler | APA 7.0 报告撰写 |
| Editor-in-Chief | Q1 期刊主编审查 |
| Devil's Advocate | 假设挑戰（3 个检查点） |
| Ethics Review Agent | AI 揭露、引用诚信 |
| Socratic Mentor | 苏格拉底引导式研究对话，含收敛准则 |
| Risk of Bias Agent | RoB 2 + ROBINS-I 偏误风险評估 |
| Meta-Analysis Agent | 效果量、異质性、森林图、GRADE |
| Monitoring Agent | Pipeline 完成后的文献监测警报 |

**模式：** full、quick、paper-review、lit-review、fact-check、socratic、**systematic-review**（新增）

### Academic Paper (v2.4)

12 个 Agent 的学术论文撰写 pipeline：

| Agent | 角色 |
|-------|------|
| Intake Agent | 组態訪談 + 上游衔接偵测 |
| Literature Strategist | 搜索策略 + 注释書目 |
| Structure Architect | 论文大纲 + 字数分配 |
| Argument Builder | 论点 + 主張-证據鏈 |
| Draft Writer | 逐章撰写 |
| Citation Compliance | 多格式引用审核 + APA↔Chicago↔MLA↔IEEE↔Vancouver 转换 |
| Abstract Bilingual | 中英双语摘要 |
| Peer Reviewer | 5 维度审查（最多 2 轮） |
| Formatter | LaTeX/DOCX/PDF 输出 — 强制 `apa7` class、XeCJK 双语、`ragged2e` 对齐修正、tectonic 编译 |
| Socratic Mentor | 逐章引导规划，含收敛准则 |
| Visualization Agent | 9 种图表類型、matplotlib/ggplot2、APA 7.0 标准 |
| Revision Coach Agent | 解析非结构化审稿意见 → 修订路线图 |

**模式：** full、plan、revision、citation-check、format-convert、bilingual-abstract、writing-polish、full-auto、**revision-coach**（新增）

### Academic Paper Reviewer (v1.4)

7 个 Agent 的多视角审查，搭配 **0-100 品质量表**：

| Agent | 角色 |
|-------|------|
| Field Analyst | 辨識領域、配置审查者 persona |
| Editor-in-Chief | 期刊适配性、新颖性、重要性 |
| Methodology Reviewer | 研究设计、统计、可重现性 |
| Domain Reviewer | 文献涵盖率、理论框架 |
| Perspective Reviewer | 跨領域观点、实务影響 |
| Devil's Advocate Reviewer | 核心论点挑戰、邏輯謬误偵测、最强反论 |
| Editorial Synthesizer | 共識分析、修订路线图、**量表評分** |

**模式：** full、re-review（验收）、quick、methodology-focus、guided

**決策对照：** ≥80 接受、65-79 小修、50-64 大修、<50 退稿

### Academic Pipeline (v2.6)

10 阶段调度器，含诚信验证、两阶段审查、苏格拉底指导、协作品质評估：

| 阶段 | Skill | 目的 |
|------|-------|------|
| 1. 研究 | deep-research | 厘清研究问题、搜索文献 |
| 2. 撰写 | academic-paper | 撰写论文初稿 |
| **2.5. 诚信审查** | **integrity_verification_agent** | **100% 引用与数據验证（v2.0：反幻觉强制令）** |
| 3. 审稿 | academic-paper-reviewer | 5 人审查（主编 + R1/R2/R3 + 魔鬼代言人） |
| → | *苏格拉底修订指导* | *引导使用者理解审稿意见* |
| 4. 修订 | academic-paper | 回应审稿意见 |
| 3'. 再审 | academic-paper-reviewer | 验收修订内容 |
| → | *苏格拉底殘餘指导* | *引导处理剩餘问题（若为 Major）* |
| 4'. 再修订 | academic-paper | 最终修订（若需要） |
| **4.5. 最终诚信审查** | **integrity_verification_agent** | **100% 最终验证（零问题要求）** |
| 5. 定稿 | academic-paper | 詢问格式风格 → MD + DOCX + LaTeX → tectonic → PDF |
| **6. 过程紀录** | **pipeline** | **论文創建过程紀录 + 协作品质評估（1–100 分）** |

**Pipeline 保证：**
- 每个阶段都需使用者确認 checkpoint
- 诚信验证（Stage 2.5 + 4.5）不可跳过
- 可重现 — 标准化流程，含完整稽核軌跡
- Pipeline 完成后自动产出协作品质評估，含 6 维度诚实評分

---

## 授權条款

本作品採用 [CC-BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) 授權。

**你可以自由：**
- 分享 — 复制及散布本作品
- 改作 — 重混、转换、以本作品为基礎进行創作

**惟須遵守以下条件：**
- **姓名标示** — 你必须给予适当的标示
- **非商业性** — 你不得将本作品用于商业目的

**标示格式：**
```
Based on Academic Research Skills by Cheng-I Wu
https://github.com/Imbad0202/academic-research-skills
```

---

## 作者

**吳政宜** (Cheng-I Wu)

---

## 更新紀录

### v2.7 (2026-03-09) — 诚信验证 v2.0：反幻觉全面改版
- **integrity_verification_agent v2.0**：Anti-Hallucination Mandate（禁止靠 AI 記憶验证）、消除灰色地带分類（仅 VERIFIED/NOT_FOUND/MISMATCH）、强制 WebSearch audit trail、Stage 4.5 独立全面验证、Gray-Zone Prevention Rule
- **已知引用幻觉 Pattern**：5 類分類法（TF/PAC/IH/PH/SH，来自 GPTZero × NeurIPS 2025 研究）、5 种复合欺騙模式、实戰案例、文献统计
- **出版后稽核**：对全部 68 篇引用做 WebSearch 逐一验证，发现 21 篇有问题（31% 错误率），证明外部查证的必要性
- **论文修正**：移除 4 篇捏造引用、修正 6 篇作者错误、修正 7 篇書目細節、修正 2 篇格式问题

### v2.6.2 (2026-03-09) — 意图匹配模式启动
- **deep-research**：苏格拉底模式改为**意图匹配**启动，取代关键字比对。支援任何语言 — 偵测含義（如「使用者想要引导式思考」）而非比对特定字串。
- **academic-paper**：Plan 模式改为**意图匹配**启动。偵测意图信号如「使用者不确定如何开始」「使用者想要逐步引导」，不限语言。
- 两个模式新增**预设规则**：当意图模糊时，偏好 `socratic`/`plan` 而非 `full` — 先引导比较安全。
- 双层架构：Layer 1（skill 启动）用双语关键字提高匹配信心；Layer 2（mode 路由）用语言無关的意图信号。

### v2.6.1 (2026-03-09) — 双语触发关键字
- **deep-research**：新增简体中文触发关键字，涵盖一般启动和苏格拉底模式。
- **academic-paper**：新增简体中文触发关键字及 Plan Mode 触发区块。
- 两份 mode selection guide 加入双语示例及中文专屬误选情境。

### v2.6 / v2.4 / v1.4 (2026-03-08) — 15+ 项改进
- **deep-research v2.3**：新增系统性文献回顾 / PRISMA 模式（第 7 模式）；3 个新 agent（risk_of_bias、meta_analysis、monitoring）；PRISMA 协议/报告模板；苏格拉底收敛准则（4 訊号 + 自动结束）；快速模式选择指南
- **academic-paper v2.4**：2 个新 agent（visualization、revision_coach）；修订追踪模板含 4 种状态；引用格式转换（APA↔Chicago↔MLA↔IEEE↔Vancouver）；统计视觉化标准；苏格拉底收敛准则；修订复原示例；**LaTeX 输出强化** — 强制 `apa7` document class、`ragged2e` + `etoolbox` 文字对齐修正、表格栏宽公式、双语摘要置中、标准字体集（Times New Roman + 思源宋体 VF + Courier New）、仅 tectonic 编译 PDF
- **academic-paper-reviewer v1.4**：0-100 品质量表含行为指标；決策对照（≥80 接受、65-79 小修、50-64 大修、<50 退稿）；快速模式选择指南
- **academic-pipeline v2.6**：自适应 checkpoint（FULL/SLIM/MANDATORY）；Phase E 宣称验证；素材护照（Material Passport）支援中途进入；跨 skill 模式顾问（14 情境）；团队协作协议；强化衔接 schema（9 个含验证规则）；诚信审查失败复原示例

### v2.4 / v1.3 (2026-03-08)
- **academic-pipeline v2.4**：新增 Stage 6 过程紀录 — 自动生成结构化论文創建过程紀录（MD → LaTeX → PDF，中英双语）；必含最后一章：**协作品质評估**，6 个维度各计 1–100 分（方向设定、智識贡献、品质把关、迭代紀律、委派效率、后设学习），含诚实回饋与改进建议；pipeline 从 9 阶段扩展为 10 阶段

### v2.3 / v1.3 (2026-03-08)
- **academic-pipeline v2.3**：Stage 5 定稿阶段现在会先詢问格式风格（APA 7.0 / Chicago / IEEE）；PDF 必须从 LaTeX 经 `tectonic` 编译（禁止 HTML-to-PDF）；APA 7.0 使用 `apa7` document class（`man` 模式）+ XeCJK 支援中英双语；字体：Times New Roman + 思源宋体 VF + Courier New

### v2.2 / v1.3 (2025-03-05)
- **跨 Agent 品质对齐**：统一定義（同儕审查、时效规则、CRITICAL 严重度、来源分级）橫跨所有 agent
- **deep-research v2.2**：synthesis 反模式、苏格拉底自动结束条件、DOI+WebSearch 验证、强化倫理诚信审查、模式转换矩陣
- **academic-paper v2.2**：4 级论证强度評分、抄襲篩查、2 个新失败路徑（F11 退稿复活、F12 研讨会转期刊）、Plan→Full 模式转换
- **academic-paper-reviewer v1.3**：DA vs R3 角色邊界、CRITICAL 判定标准、共識分類（4/3/SPLIT/DA-CRITICAL）、信心分数加權、亞洲与区域期刊參考
- **academic-pipeline v2.2**：checkpoint 确認语意、模式切换矩陣、技能失败降级策略、状态所有權协议、素材版本控制

### v2.0.1 (2026-03)
- **精简 4 个 SKILL.md**（-371 行, -16.5%）：移除跨 skill 重复、内嵌模板改为档案引用、冗餘路由表、重复模式选择区块
- 修复 academic-paper 与 academic-pipeline 之間修订迴圈上限的矛盾

### v2.0 (2026-02)
- **academic-pipeline v2.0**：5→9 阶段、强制诚信验证、两阶段审查、苏格拉底修订指导、可重现性保证
- **academic-paper-reviewer v1.1**：+魔鬼代言人审查者（第 7 agent）、+re-review 模式（验收）、+审后苏格拉底指导
- 新增 agent：`integrity_verification_agent` — 100% 引用/数據验证，含稽核軌跡
- 新增 agent：`devils_advocate_reviewer_agent` — 8 维度论点挑戰
- 输出順序：MD + DOCX → 詢问 LaTeX → 确認 → PDF

### v1.0 (2026-02)
- 初版发布
- deep-research v2.0（10 agents、6 模式含 socratic）
- academic-paper v2.0（10 agents、8 模式含 plan）
- academic-paper-reviewer v1.0（6 agents、4 模式含 guided）
- academic-pipeline v1.0（调度器）
