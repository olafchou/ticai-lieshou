# Stock Catalyst Hunter

`Stock Catalyst Hunter` 是一个面向支持 skill 的 agent 环境的 A 股题材映射技能。

它接收一段新闻、传闻、政策变化、突发事件或截图，不做冗长新闻总结，而是直接把事件映射成更可能相关的 A 股方向和个股，并用简洁表格给出概率、时间维度和分析理由。

## 适合做什么

- 输入一条新闻，找出可能受影响的 A 股题材和股票
- 输入一张财经截图，提取事件后映射到 A 股方向
- 区分硬逻辑和题材炒作
- 用更接近盘面的方式输出，而不是写成长篇研报

## 输出风格

- 先给事件结论
- 再给主要受益方向和风险方向
- 再用表格列出相关股票
- 分析理由简洁直给，不在正文堆长来源引用
- 不展示“核心信息提取”这类中间过程表

## 仓库结构

```text
.
├── README.md
├── docs/
│   └── superpowers/
│       ├── plans/
│       └── specs/
└── ticai-lieshou/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    └── examples.md
```

## 安装方式

### 方式 1：通过 SkillHub 安装

[Stock Catalyst Hunter - SkillHub](https://skillhub.tencent.com/skills/ticai-lieshou)

### 方式 2：通过 GitHub 手动安装

适合想自己维护、调试或二次修改的用户。

#### 方式 A：直接对话安装

如果你的龙虾 / OpenClaw 支持让助手根据 GitHub 仓库安装 skill，可以直接发送：

```text
https://github.com/olafchou/stock-ticai-lieshou 帮我安装一下这个skill
```

这是最省事的 GitHub 安装方式。

#### 方式 B：手动复制到本地 skills 目录

根据 OpenClaw 官方文档，技能可以放到以下目录之一：

- 当前工作区的 `skills/`
- `~/.openclaw/skills/`
- `~/.agents/skills/`
- 当前工作区的 `.agents/skills/`

安装步骤：

1. 克隆仓库：

```bash
git clone https://github.com/olafchou/stock-ticai-lieshou.git
cd stock-ticai-lieshou
```

2. 把 `ticai-lieshou/` 目录复制到你的 OpenClaw 技能目录，例如：

```bash
mkdir -p ~/.openclaw/skills
cp -R ./ticai-lieshou ~/.openclaw/skills/ticai-lieshou
```

3. 重新启动会话，或重新加载 skills，让新技能出现在当前环境里。

### 安装后怎么使用

安装完成后，用这类意图触发：

```text
这条新闻利好哪些A股
这消息对应什么题材股
这个事件会炒哪些股票
这张截图会带动哪些A股
```

## 主要文件

- `ticai-lieshou/SKILL.md`
  - skill 主说明，定义触发意图、工作流、输出格式和约束
- `ticai-lieshou/agents/openai.yaml`
  - UI 元数据和默认提示
- `ticai-lieshou/examples.md`
  - 更适合 GitHub 浏览的示例输入输出

## 推荐触发意图

这类表达最适合触发 `题材猎手`：

- `这条新闻利好哪些A股`
- `这消息对应什么题材股`
- `这个事件会炒哪些股票`
- `这张截图会带动哪些A股`
- `帮我找这条消息的相关A股`

## 示例

文字输入：

```text
这条新闻利好哪些A股：美加墨世界杯赛程出炉，揭幕战将于6月12日3点举行。
```

图片输入：

```text
帮我看看这张图会影响哪些A股股票。
```

## 设计原则

- 不维护本地概念股数据库
- 先搜索市场映射，再做推理判断
- 少给废票，宁可少给也不乱凑名单
- 输出重点是找方向和找票，不是做真假鉴定报告

## 当前状态

当前版本：`1.1.0`

这一版已经包含：

- 核心 skill
- 图片输入分析模板
- 搜索失败降级策略
- 多个示例输入输出
- 事件合理性判断下沉到补充说明
- 移除“核心信息提取”这类中间展示风格

当前已发布平台：

- SkillHub

当前未发布平台：

- ClawHub

后续可以继续补：

- 发布平台适配元数据
- 更多事件案例
- 更强的“短线题材 / 中线逻辑”分层输出
