# wcskill

望川的学员内容创作工具箱。当前提供 6 个 Skill：一个入口、四项内容与学习能力和一项更新工具。

## 工具

| Skill | 功能 | 输入 | 输出 |
| --- | --- | --- | --- |
| `wc` | 工具箱入口 | 你当前想完成的任务 | 合适的工具及所需材料 |
| `wc-organize` | 短视频语料整理 | 含正文和各项数据的短视频 CSV | 原始数据表、气口断行稿、开局／交付／收束分区、首拍片段与机制对照表 |
| `wc-dy-hook` | 抖音开头分析与生成 | 对标文案和数据表；或正文与已有范式库 | 开头范式库，或 5–10 个备选开头 |
| `wc-xhs-title` | 小红书标题生成 | 话题／正文及目标受众 | 从 62 套结构中匹配的标题方案 |
| `wc-research` | 思想家研究圆桌 | 一个问题、主题或材料；可指定人物或沿用已有圆桌 | 独立观点、交叉回应、主持审议及研究依据；也可转入知识讲解与持续学习 |
| `wc-update` | 一句话更新工具箱 | “帮我更新 wcskill” | 更新当前客户端的正式工具，备份本地修改，保留用户存档 |

## 安装

对 AI 说：

> 帮我从 https://github.com/Rivo2026/wcskill 安装 wcskill，按仓库 INSTALL.md 安装到当前客户端。

这会安装整套工具箱。WorkBuddy、Codex 和 Claude Code 的安装步骤见 [安装入口](INSTALL.md)，由助手执行，学员不用逐个下载子工具。

只说“安装 wcskill”需要当前助手能检索到本仓库，或所用技能市场已收录这个名字；本仓库不承诺所有客户端都已收录。找不到时补上上述仓库链接即可。

使用 Skills CLI 将全部工具安装到 Codex，或只安装语料整理工具：

```bash
DISABLE_TELEMETRY=1 npx -y skills add Rivo2026/wcskill --skill '*' --agent codex -g --yes
DISABLE_TELEMETRY=1 npx -y skills add Rivo2026/wcskill --skill wc-organize --agent codex -g --yes
```

Claude Code 用户把 `--agent codex` 改为 `--agent claude-code`。命令使用 [Skills CLI](https://github.com/vercel-labs/skills)，需要 Git、Node.js 和 npm/npx；安装与更新命令关闭其匿名使用统计。

也可以下载本仓库，或运行 `git clone https://github.com/Rivo2026/wcskill.git`，把 `skills/` 下的 6 个文件夹分别放进所用客户端的 Skill 目录。每个文件夹里应直接包含 `SKILL.md`，并保留随附的 `references/`、`scripts/`、`agents/`。

| 客户端 | 用户级 Skill 目录 | 调用示例 |
| --- | --- | --- |
| Codex | `~/.agents/skills/` 或 `~/.codex/skills/`，选一个入口即可 | `$wc`、`$wc-organize` |
| Claude Code | `~/.claude/skills/` | `/wc`、`/wc-organize` |
| WorkBuddy | `~/.workbuddy/skills/` | 用中文说明任务，或在技能列表选中 `wc` |

### WorkBuddy 安装

直接把上面的一句话发给 WorkBuddy，由它读取 [INSTALL.md](INSTALL.md) 并安装六个工具。以下下载方式仅作备用。

也可以下载 [WorkBuddy 整套安装包](https://github.com/Rivo2026/wcskill/releases/download/v2.3.0/wcskill-workbuddy-2.3.0.zip)，解压后把文件夹交给 WorkBuddy，并说：

> 请读取安装说明，用随附的 install.py 将这套 wcskill 安装到 WorkBuddy，保留我的存档和已有修改。

也可以在解压后的文件夹中运行 `python3 install.py --source .`；Windows 使用 `py -3 install.py --source .`。需要 Python 3.9+。安装器默认写入 `~/.workbuddy/skills/`，安装前备份同名旧内容，失败时恢复原入口。若提示未标识来源的同名工具，确认它们属于旧版 wcskill 后才加 `--replace-existing`。

从 GitHub 下载或克隆了本仓库的用户，也可以在仓库目录运行：

```bash
python3 skills/wc-update/scripts/workbuddy_install.py --source .
```

喜欢界面导入的学员，可以在 [发布页](https://github.com/Rivo2026/wcskill/releases/tag/v2.3.0) 下载六个单独的 WorkBuddy 技能 ZIP 包，通过“技能 → 添加技能 → 上传技能”逐个导入。整套安装包用于解压安装，不作为单个 Skill 上传。导入后在“已安装”中确认启用，再新建对话说“望川工具箱有哪些工具”。[WorkBuddy 官方安装说明](https://www.codebuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Skills-Market)

WorkBuddy 包由同一套核心 Skill 自动生成，保留正文、参考资料和脚本，并补充导入所需的中文介绍、英文介绍、版本和作者信息。`wc` 是总入口，整套使用需要安装全部六个 Skill。

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

$wc-dy-hook 从这份对标文案和播放数据表里提炼开头范式。

$wc-xhs-title 给这篇文章起小红书标题，目标读者是刚开始做内容的创作者。

$wc-research 帮我为这个问题推荐一组思想家，共同研究不同解释与依据。
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

语料整理中的结构标注属于工作视图，仍需要结合原文复核。

## 知识研究圆桌

`wc-research` 组织社会学、哲学、传播学、心理学与消费研究人物的模拟圆桌。内置戈夫曼、布迪厄、杜威、维特根斯坦、麦克卢汉、霍尔、卡尼曼、班杜拉、西奥迪尼和贝尔克的方法卡，按问题推荐 3–5 位；也可以直接指定人物或让工具代选并开始。首次未确定阵容时，先确认人选。

每人先独立研究，主持人提取关键分歧，再把具体判断交给人物互相质询和回应，最后审议依据、修订与未决问题。继续追问时沿用同组人物和上一轮立场；输入“结束圆桌”即可退出。人物发言是根据公开框架进行的模拟分析，原著观点、当代应用和核实事实分别说明。

遇到不懂的概念可以插入讲解，也能从一段内容反推知识地图，再按实际回答持续陪学。要求保存课题时，记录人物、分歧、证据、讲解和进度，下次从实际停下的位置继续。

完整圆桌需要客户端提供并允许独立子代理工具。不支持时会说明情况，可改用单助手多视角模拟；不会把这种执行方式称为独立代理讨论。

```text
$wc-research 你来选人直接开始，研究“为什么觉得一篇内容有用，却迟迟没有行动”。
$wc-research 让戈夫曼、杜威、霍尔和卡尼曼共同研究这个问题，并互相回应。
$wc-research 从这篇文章的具体判断出发，帮我梳理值得学的知识和必要基础，先给知识地图。
$wc-research 带我从零学习这个主题，每轮讲一个知识点，根据我的回答调整。
$wc-research 继续上次圆桌，让原来那组人回应我补充的这个反例。
```

## 一句话更新

安装包含 `wc-update` 的版本并新建对话后，直接对助手说：

> 帮我更新 wcskill

也可以在 Codex 中输入 `$wc-update`，或在 Claude Code 中输入 `/wc-update`。工具会沿用当前客户端和安装范围，更新本仓库的正式 Skill；更新前备份将被覆盖的内容，保留用户存档和其他来源的 Skill。本地修改会留在备份中，不自动合并进新版。

WorkBuddy 同样可以说“帮我更新 wcskill”，会使用随附的 Python 安装器下载官方最新版并写入 WorkBuddy 的实际技能目录。只检查新版时不改文件。它使用独立的 WorkBuddy 分支，不要求 Skills CLI 识别这个客户端。

早期版本没有更新入口：先重新运行上面的完整安装命令，或对助手说“从 https://github.com/Rivo2026/wcskill 安装最新版到当前客户端，保留我的存档和本地修改”。只安装单个内容 Skill 的用户，也需要补装 `wc-update` 才能使用这个入口。只询问版本或更新内容不会执行安装。

更新完成后，如果当前对话仍使用旧规则，新建一次对话即可。完整流程见 [更新 Skill](skills/wc-update/SKILL.md)。

## 许可证

[MIT License](LICENSE)
