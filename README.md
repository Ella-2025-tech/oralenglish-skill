# oralenglish-skill

专四（TEM-4）英语口语思辨陪练 Skill：AI 逐轮抛出英文思辨 Topic 并给出正反参考句型，用户口头作答后获得「原句转写 → 中式英语优化 → 简短点评」的结构化反馈，通过【继续】与【重新回答】循环训练。

## 1. 项目解决什么问题

备考专四口语的学习者普遍存在三类痛点：**口语表达不地道**（中式英语多：中文直译语序、中式搭配、逻辑断层、母语负迁移）、**缺乏思辨训练**（只会背诵、不会正反论证）、**缺少即时结构化反馈**（练完不知道哪里错了、怎么改）。本项目用一套**纯对话式陪练流程**解决这些问题：AI 先给思辨话题和可模仿的正反句型作为脚手架，用户开口作答后，AI 立即给出"原句 + 优化句 + 点评"的针对性反馈，并通过【继续】追问 /【重新回答】重练来强化改正，让学习者反复开口、即时纠错、逐步摆脱中式英语。

## 2. 主要功能

- **逐轮出题**：每轮给 1 个英文思辨 Topic + 2 句参考句型（一句肯定立场、一句否定立场，纯英文），作为作答脚手架。
- **【我的原句】**：原样转写用户口述英文，保留原始表达，不做任何润色纠错。
- **【优化句】**：只生成 1 版适配专四口语的改写，优先修正中式英语（直译语序 / 中式搭配 / 逻辑断层 / 母语负迁移），**拒绝浅层同义词替换**，优化句式逻辑，适配口头表达不过度书面化，核心改动加粗。
- **【简短点评】**：点明本次中式英语的具体问题，并简评逻辑、句式、用词地道度。
- **循环选项**：反馈后提供【继续】（当前话题深度追问，开启新一轮）与【重新回答】（不换话题，再答一次，循环直到选择继续）。
- **纯对话式**：不依赖任何外部工具；暂不支持网页抓取、PDF、图形界面。

## 3. 安装方法

本 Skill 是**纯指令型**（无脚本、无第三方运行时依赖），安装即"放入目录 + 宿主环境识别"。

- **方式一（推荐）**：将整个 `oralenglish-skill/` 目录放入宿主 Agent 的 Skill 目录，例如 `workspace/.user_skills/oralenglish-skill`（路径以宿主环境为准），宿主自动识别 `SKILL.md`。
- **方式二**：按平台规范直接引用该目录，或让 Agent 读取其中的 `SKILL.md` 后按指令执行。

前置条件：
- 需要一个支持 Skill 的 AI Agent 宿主环境（如豆包/豆包办公）。
- 无需安装 Python 包即可运行 Skill 本体。
- 仅**本地开发校验**（可选）需要 Python 3 与 `pyyaml`：

```bash
pip install pyyaml
```

## 4. 使用方法

1. 对 Agent 说一句训练指令即可触发，例如：
   - "用 oralenglish-skill 陪练我练口语"
   - "开始一轮专四口语思辨训练"
2. 按回合进行：
   - AI 给出 **Topic** 与 **参考句型（正 / 反）** → 你口头作答（可语音转文字或直接输入口语原文）。
   - AI 输出 **①【我的原句】②【优化句】③【简短点评】** → 你选择 **【继续】** 或 **【重新回答】**。
   - 【继续】= 当前话题深度追问，进入新一轮；【重新回答】= 同一话题再答一次，重新获得三段反馈。

## 5. 输入输出示例

### 第 1 轮：AI 出题

> **Topic**: Should college students take part-time jobs during their studies?
> **Reference Sentences**:
> - 肯定：*I believe part-time jobs are valuable because they give students real work experience and teach them to manage their time.*
> - 否定：*On the other hand, part-time jobs can distract students from their studies and leave them too tired to focus in class.*

### 用户口头作答（输入）

> I think take part-time job is good, because it can let me learn many knowledge and also can make me happy.

### AI 反馈（输出）

> **①【我的原句】**
> I think take part-time job is good, because it can let me learn many knowledge and also can make me happy.
>
> **②【优化句】**
> I think **taking** part-time **jobs** is **a good idea**, because it **gives us a chance to gain practical experience and broadens our horizons**, and it also **keeps us motivated**.
>
> **③【简短点评】**
> 本次中式英语问题主要是中式搭配：`learn knowledge`（"学知识"直译）应改为 `gain experience`；`take part-time job` 缺少动名词作主语、属省略主语的直译语序。逻辑上因果清楚但理由单薄；句式偏口语碎句；用词 `make me happy` 过于随意，可换更地道的表达。
>
> 请选择：**【继续】**（深度追问本轮话题）或 **【重新回答】**（同一 Topic 再答一次）。

## 目录结构

```
English/                          # 项目根目录
├── README.md                     # 本文件（介绍 / 用法 / 示例）
└── oralenglish-skill/            # Skill 本体
    ├── SKILL.md                  # 运行指令：流程、规范、示例、边界
    └── agents/
        └── openai.yaml           # OpenAI AgentKit 开源元数据
```

## 本地开发与验证

```bash
# 校验 SKILL.md frontmatter 与命名（需要 pyyaml）
python <skill-creator>/scripts/quick_validate.py oralenglish-skill
```

当前为本地开发版本，尚未初始化 Git、未上传 GitHub。
