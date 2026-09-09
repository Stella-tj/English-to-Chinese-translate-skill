# 英文翻译与提取高频词汇

[English](README.md)

帮助中文用户看懂英文、记住实用词汇的 skill，兼容 Codex 和 Claude Code。支持英文截图、句子和文章，按顺序输出：**翻译 → 常用词**。

执行规则用英文编写，翻译结果、解释和词义默认使用简体中文。

## 使用

直接发送英文截图，或输入：

```text
翻译：We should prioritize sustainable growth.
```

在 Codex 中也可以明确调用：

```text
$english-to-chinese-study 翻译：We should prioritize sustainable growth.
```

支持临时调整，如“只选两个单词”“这次只要自然翻译”。用户明确提出的其他任务优先，例如截图调试不会被强行改成翻译。查看[完整输出示例](examples/translation.md)。

## 设计要点

- 只提供一次完整、自然的中文翻译。
- 固定短语说明整体意思，不把错误的字面拼接当作正确翻译。
- 译文保留否定、条件、数字和语气，不用摘要代替全文。
- 词表排除 is、dog、table、work 等基础独立词；有学习价值的完整短语可以收录。
- “常用词”表格仅含“单词 / 短语”“文中含义”“记忆搭配（含中文）”三列，不附词性或末尾回忆提示。
- 截图看不清或被裁切时明确标记，不猜测缺失内容。

自动触发由模型根据描述匹配，并非强制关键词开关；没有自动匹配时可用上面的明确调用方式。

## 安装

这是纯指令 skill，无需额外 API 密钥、Python 或连接器。处理截图需要支持图片理解的宿主与模型。

下载或克隆仓库，把 `SKILL.md` 和 `agents` 文件夹放入个人技能目录下的 `english-to-chinese-study` 文件夹中。

[当前 Codex 文档](https://learn.chatgpt.com/docs/build-skills)列出的个人目录为 `~/.agents/skills`，项目目录为 `.agents/skills`。部分已有安装也会读取 `~/.codex/skills`，本技能已在该目录完成本地安装并被发现。选择当前安装支持的一个位置即可，避免重复安装；未显示时可重启 Codex。

也可以直接把下面这段话发给 Codex：

```text
使用 $skill-installer 安装 https://github.com/Stella-tj/English-to-Chinese-translate-skill 中的 skill。技能位于仓库根目录，请以 english-to-chinese-study 为安装目录名。
```

### Claude Code

将 `SKILL.md` 放到个人目录 `~/.claude/skills/english-to-chinese-study/SKILL.md`，或项目内的 `.claude/skills/english-to-chinese-study/SKILL.md`。不需要 Codex 专用的 `agents/openai.yaml`。

明确调用方式：

```text
/english-to-chinese-study 翻译：We should prioritize sustainable growth.
```

参见 [Claude Code 官方说明](https://code.claude.com/docs/en/skills)。兼容性依据文档格式确认，尚未在 Claude Code 中独立实测。

## 维护与分享

`SKILL.md` 是核心规则，`agents/openai.yaml` 是显示信息和自动调用配置。其余文件面向读者与维护者，不需要每次翻译时加载。

[行为检查用例](evals/cases.md)覆盖习语、否定句、基础词过滤、截图和触发边界。修改后可在新对话中逐项尝试；文件格式检查通过不代表翻译质量和自动触发已经全部实测。

沿用仓库所有者选择的 [MIT 许可证](LICENSE)。
