# English to Chinese Study

[简体中文](README.zh-CN.md)

将英文截图或文本翻译成中文，并提炼常用词汇，附中文释义和实用搭配，过滤过于基础的单词。支持 Codex 和 Claude Code。

An instruction-only skill compatible with Codex and Claude Code for understanding English and remembering useful vocabulary. Send English screenshots, sentences, or articles to get **natural Chinese translation → common vocabulary**.

The execution instructions are written in English. Translations, explanations, and vocabulary meanings default to Simplified Chinese.

## Usage

Upload an English screenshot, or send:

```text
翻译：We should prioritize sustainable growth.
```

To explicitly select the skill in Codex:

```text
$english-to-chinese-study 翻译：We should prioritize sustainable growth.
```

Customize the response with instructions such as `只选两个单词` or `这次只要自然翻译`. See a [complete example](examples/translation.md).

## Behavior

- Provides one complete, natural Chinese translation.
- Explains idioms and phrasal verbs without teaching misleading literal meanings.
- Preserves negation, conditions, numbers, and uncertainty in natural Chinese.
- Selects useful non-basic vocabulary; skips standalone words such as `is`, `dog`, `table`, and `work`.
- Uses three vocabulary columns: word/phrase, contextual meaning, and a bilingual collocation. No part-of-speech column or closing recall prompt.
- Marks unreadable or cropped screenshot text instead of guessing.
- Respects explicit tasks: a debugging screenshot does not automatically become a translation exercise.

Automatic invocation is model-selected from the description, not a guaranteed keyword hook. Use explicit invocation when automatic selection does not occur.

## Installation

This is an instruction-only skill. It requires no additional API key, Python environment, or connector. Screenshots require a host/model that can read images.

Download or clone this repository. Copy `SKILL.md` and the `agents` directory into a folder named `english-to-chinese-study` under your personal skill directory:

```text
<personal-skill-directory>/
└── english-to-chinese-study/
    ├── SKILL.md
    └── agents/
        └── openai.yaml
```

Current [Codex documentation](https://learn.chatgpt.com/docs/build-skills) lists `~/.agents/skills` for user-wide skills and `.agents/skills` for repository-local skills. Existing Codex installations may also load `~/.codex/skills`; this skill was locally installed and discovered there. Use one supported location, avoiding duplicate installations. If the skill does not appear, restart Codex.

You can also ask Codex:

```text
Use $skill-installer to install the skill from https://github.com/Stella-tj/English-to-Chinese-translate-skill. The skill is at the repository root; install it under the name english-to-chinese-study.
```

### Claude Code

Copy `SKILL.md` into `~/.claude/skills/english-to-chinese-study/SKILL.md` for personal use, or `.claude/skills/english-to-chinese-study/SKILL.md` inside a project. The Codex-specific `agents/openai.yaml` is not required.

Invoke it with:

```text
/english-to-chinese-study 翻译：We should prioritize sustainable growth.
```

See the [Claude Code skill documentation](https://code.claude.com/docs/en/skills). Compatibility is based on the documented format; this release has not been independently tested in Claude Code.

## Repository layout

```text
SKILL.md                   Execution instructions and trigger description
agents/openai.yaml         Display metadata and invocation policy
README.md                  English documentation
README.zh-CN.md            Chinese documentation
examples/translation.md    Illustrative translation output
evals/cases.md             Manual behavior checks for maintainers
```

Only `SKILL.md` and `agents/openai.yaml` are needed at runtime. Examples and evaluation cases are contributor documentation, not instructions to load for every translation.

## Maintenance

Keep execution instructions in English and output examples in Chinese. Try the [evaluation cases](evals/cases.md) in fresh conversations after changing behavior. Judge meaning and coverage rather than exact wording. Format validation does not establish translation quality or trigger reliability.

Licensed under the [MIT License](LICENSE), as selected by the repository owner.
