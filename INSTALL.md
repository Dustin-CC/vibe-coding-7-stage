# 安装与使用

这是 `vibe-coding-7-stage` Skill（展示名称：Vibe Coding 七阶段开发），根据用户粘贴的《Vibe Coding 七阶段开发流程（需求 → 设计 → 开发 → 验收）》整理，保留原定七阶段与六个审核节点，未额外插入独立代码审查阶段。七条提示词做了精简，共用规则集中维护；补充明确了跳转、授权延续、上下文恢复及验收证据的执行含义。

## 文件

```text
vibe-coding-7-stage/
├── SKILL.md                    入口、阶段、修改权限与输出规则
├── agents/openai.yaml          显示名称与默认调用提示
├── references/stages.md        七条阶段提示词、精简产出和审核重点
├── references/review-rules.md  六个审核节点、返回/继续和验收判定
└── INSTALL.md                  本说明
```

纯指令 Skill，使用时无需安装 Python、依赖或连接外部服务。

## 安装

当前官方用户级发现目录为 `~/.agents/skills`；本机亦存在此目录。本次交付的实际安装结果以聊天中的最终报告为准，文件包本身不表示已安装。

若尚未安装，在解压后包含 `vibe-coding-7-stage` 文件夹的目录打开终端，执行：

```sh
mkdir -p "$HOME/.agents/skills"
if test -e "$HOME/.agents/skills/vibe-coding-7-stage" || test -L "$HOME/.agents/skills/vibe-coding-7-stage"; then
  echo '同名 Skill 已存在，请先检查并备份后再更新。'
else
  cp -R ./vibe-coding-7-stage "$HOME/.agents/skills/"
fi
```

最终结构应为 `~/.agents/skills/vibe-coding-7-stage/SKILL.md`，不要多套一层文件夹。

如果只供一个代码仓库使用，将整个文件夹放到该仓库的 `.agents/skills/vibe-coding-7-stage/`。用户级与项目级二选一，避免同名重复显示。本机已有其他 Skill 放在 `~/.codex/skills`，本包采用当前官方文档列出的 `.agents/skills` 路径，无需搬动其他 Skill 或改全局配置。

Codex 会自动检测 Skill 变化；若尚未显示，重启后在项目会话中使用 `$vibe-coding-7-stage`，或在 Skill 选择器中查找“Vibe Coding 七阶段开发”。文件存在仅证明安装完成，是否被当前会话发现仍以选择器或实际调用为准。

官方依据：[OpenAI：Build skills](https://learn.chatgpt.com/docs/build-skills)，核对日期：2026-10-23。

## 使用

在目标项目中开启会话，发送：

```text
请使用 $vibe-coding-7-stage。
我有一个新需求：【用大白话描述需求】。
请结合当前项目，从需求理解阶段开始。
```

也可自然语言触发：“我有一个新需求：XXX，请按 Vibe Coding 七阶段标准开发流程，从需求理解开始。”普通直接改代码的请求不会被强制套进本流程。

阶段结束后按需要回复：

```text
通过，进入下一阶段
需要修改：补充网络中断时的用户提示
返回第 1 阶段：本次不包含批量操作
```

完整顺序：需求理解 → 概要方案 → 详细设计 → 开发计划 → 编码实现 → 测试验收 → 交付总结。第 1～4 阶段只读；批准开发计划并要求进入下一阶段后才开始编码。

省略阶段需确认路线，例如：“这是文案小改动，按需求 → 开发 → 验收 → 交付的简化流程执行，各节点仍等我确认。”

需要连续执行时明确授权范围，例如：“开发计划通过，请连续完成编码和测试，测试结束后等我审核。”已有授权会延续，不要求每个开发任务再确认。

## 与项目规范配合

Skill 负责阶段、提示词、审核与输出；项目 `AGENTS.md` 及已有文档继续负责架构、业务规则、命名和测试命令；具体需求与确认保留在当前会话。

无需先改项目 `AGENTS.md` 才能使用。只有你明确要求将共用规则写入项目时才合并，保留原有规范，避免重复，也不将本工作流强制用于所有日常编程任务。切换会话时提供已有确认记录或项目中已授权保存的成果，Skill 不会自动恢复其他会话的批准状态。

## 更新与移除

更新前先对照同名目录并备份，再替换为新版，避免叠放成嵌套目录。移除时只移走自己安装的 `vibe-coding-7-stage` 文件夹；不需要删除项目文件或改变其他 Skill。
