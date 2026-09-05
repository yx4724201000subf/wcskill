# wcskill

望川的学员内容创作工具箱。当前提供 5 个 Skill：一个入口和四项创作能力。

## 工具

| Skill | 功能 | 输入 | 输出 |
| --- | --- | --- | --- |
| `wc` | 工具箱入口 | 你当前想完成的任务 | 合适的工具及所需材料 |
| `wc-corpus` | 语料纠错与气口断行 | 文案 CSV／Markdown | 断行文案、开局／交付／收束标记、存疑表与纠错清单 |
| `wc-coin` | 概念造词 | 要重定义的概念和现有误解 | 5 个候选词、换框句、自评与 1–2 个推荐 |
| `wc-dy-hook` | 抖音开头分析与生成 | 对标文案和数据表；或正文与已有范式库 | 开头范式库，或 5–10 个备选开头 |
| `wc-xhs-title` | 小红书标题生成 | 话题／正文及目标受众 | 从 62 套结构中匹配的标题方案 |

## 安装

下载本仓库，或在终端运行：

```bash
git clone https://github.com/yx4724201000subf/wcskill.git
```

把 `skills/` 下的 5 个文件夹分别放进所用客户端的 Skill 目录。每个文件夹里应直接包含 `SKILL.md`，并保留随附的 `references/`、`scripts/`。

| 客户端 | 用户级 Skill 目录 | 调用示例 |
| --- | --- | --- |
| Codex | `~/.codex/skills/` | `$wc`、`$wc-corpus` |
| Claude Code | `~/.claude/skills/` | `/wc`、`/wc-corpus` |

本版抖音开头 Skill 名称是 `wc-dy-hook`。旧版使用 `wc-hook-dy`，升级时请用新名称替换旧入口。

## 怎么开始

可以先调用入口，把任务直接说出来：

```text
$wc 我有一份对标账号文案，想先纠错，再按照口播气口换行。
```

也可以直接使用具体工具：

```text
$wc-corpus 处理这份 CSV，作者是××，全部处理；正文是原始转写，请先纠错再断行。

$wc-coin 我要给“明明在忙，但没有推进真正重要的事”这个现象造词。观众通常把它理解成努力，我想指出忙碌和有效进展的区别。

$wc-dy-hook 从这份对标文案和播放数据表里提炼开头范式。

$wc-xhs-title 给这篇文章起小红书标题，目标读者是刚开始做内容的创作者。
```

Claude Code 用户把示例中的 `$` 改为 `/`。

## 表格依赖

抖音开头工具附带 `scripts/table_to_md.py`，用 Python 3 读取表格。CSV、TSV 使用标准库；读取 XLSX、XLSM 时需安装 `openpyxl`：

```bash
python3 -m pip install openpyxl
```

造词工具交付候选与自评；独立的模拟反应测评不在本包内。语料整理中的结构标注属于工作视图，仍需要结合原文复核。

## 许可证

[MIT License](LICENSE)
