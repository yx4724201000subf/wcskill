# wcskill

望川的学员内容创作工具箱。当前提供 5 个 Skill：一个入口和四项创作能力。

## 工具

| Skill | 功能 | 输入 | 输出 |
| --- | --- | --- | --- |
| `wc` | 工具箱入口 | 你当前想完成的任务 | 合适的工具及所需材料 |
| `wc-organize` | 短视频语料整理 | 含正文和各项数据的短视频 CSV | 原始数据表、气口断行稿、开局／交付／收束分区、首拍片段与机制对照表 |
| `wc-coin` | 概念造词 | 要重定义的概念和现有误解 | 5 个候选词、换框句、自评与 1–2 个推荐 |
| `wc-dy-hook` | 抖音开头分析与生成 | 对标文案和数据表；或正文与已有范式库 | 开头范式库，或 5–10 个备选开头 |
| `wc-xhs-title` | 小红书标题生成 | 话题／正文及目标受众 | 从 62 套结构中匹配的标题方案 |

## 安装

使用 Skills CLI 安装全部工具，或只安装语料整理工具：

```bash
npx -y skills add Rivo2026/wcskill -g --all
npx -y skills add Rivo2026/wcskill -g --skill wc-organize --agent codex --yes
```

也可以下载本仓库，或运行 `git clone https://github.com/Rivo2026/wcskill.git`，把 `skills/` 下的 5 个文件夹分别放进所用客户端的 Skill 目录。每个文件夹里应直接包含 `SKILL.md`，并保留随附的 `references/`、`scripts/`。

| 客户端 | 用户级 Skill 目录 | 调用示例 |
| --- | --- | --- |
| Codex | `~/.agents/skills/` 或 `~/.codex/skills/`，选一个入口即可 | `$wc`、`$wc-organize` |
| Claude Code | `~/.claude/skills/` | `/wc`、`/wc-organize` |

本版抖音开头 Skill 名称是 `wc-dy-hook`。旧版使用 `wc-hook-dy`，升级时请用新名称替换旧入口。

语料整理工具由 `wc-corpus` 改名为 `wc-organize`，现在仅接收短视频 CSV。升级后请移除旧 `wc-corpus` 的安装入口，避免继续调用旧输出格式；`wcz-corpus` 是独立的自用工具，不受此改名影响。

## 怎么开始

可以先调用入口，把任务直接说出来：

```text
$wc 我有一份短视频 CSV，想保留数据并按照口播气口换行。
```

也可以直接使用具体工具：

```text
$wc-organize 处理这份短视频 CSV，保留全部记录和各项数据，整理成断行 Markdown，放在同目录。

$wc-coin 我要给“明明在忙，但没有推进真正重要的事”这个现象造词。观众通常把它理解成努力，我想指出忙碌和有效进展的区别。

$wc-dy-hook 从这份对标文案和播放数据表里提炼开头范式。

$wc-xhs-title 给这篇文章起小红书标题，目标读者是刚开始做内容的创作者。
```

Claude Code 用户把示例中的 `$` 改为 `/`。

## 语料整理的输出

每个 CSV 生成一份 `原文件名·断行整理版.md`，默认处理全部记录。每篇先用普通表格保留原字段与原值，再按气口断行，使用独立的“开局、交付、收束”标题。开局下方用“对应片段｜截停机制”小表，明确标出第一拍哪里用了什么机制。

不生成存疑表、清洗改动清单、判断说明、校验附录或折叠 JSON。清洗只处理证据明确的转写错误，源 CSV 保持不变；空正文保留数据并标明未做断行。数据与正文拼回由脚本校验，段界和机制仍需语义复核。

## 表格依赖

语料整理工具的 `scripts/render_corpus.py` 只依赖 Python 3 标准库。

抖音开头工具附带 `scripts/table_to_md.py`，用 Python 3 读取表格。CSV、TSV 使用标准库；读取 XLSX、XLSM 时需安装 `openpyxl`：

```bash
python3 -m pip install openpyxl
```

造词工具交付候选与自评；独立的模拟反应测评不在本包内。语料整理中的结构标注属于工作视图，仍需要结合原文复核。

## 许可证

[MIT License](LICENSE)
