# design-to-frontend

让 Opus 定稿，让 Gemini 按稿实现。用同一页可运行的设计样板和截图，把设计决策交到编码模型手里，避免落地时重新发明一套版式。

| 阶段 | 建议使用 | 产出 |
| --- | --- | --- |
| `design` | Claude Opus 5.5 | 一页可运行的样板、桌面和移动端截图、交接说明 |
| `implement` | Gemini 4 Carbon，或使用 Hydrogen / Argon | 按定稿实现目标页面，保留项目技术栈并验证交互 |
| `review` | Claude Opus 5.5，或你指定的模型 | 按优先级列出实现与定稿的差异 |

## 安装到 Antigravity

打开 [SKILL.md](./SKILL.md)，用 **Raw** 保存为 `SKILL.md`，放进项目的 `.agents/skills/design-to-frontend/` 目录。仓库只有这一个文件是运行所必需的。

```text
your-project/
└── .agents/
    └── skills/
        └── design-to-frontend/
            └── SKILL.md
```

如果想在 Antigravity App 的所有项目中使用，放到 `~/.gemini/config/skills/design-to-frontend/SKILL.md`。也可参照 [Antigravity 官方安装说明](https://antigravity.google/docs/skills) 放入不同客户端的技能目录。

## 用法

**1. 选 Opus，先做一页样板**

```text
/design-to-frontend design 给我的作品集做一版首页样板，先别改现有页面。
```

默认交接目录是 `design-handoff/<page>/`，内含可运行的样板、截图和 `handoff.md`。

**2. 确认样板后，切到 Gemini 按稿实现**

```text
/design-to-frontend implement 读取 design-handoff/home/handoff.md，按定稿实现首页，保留现有技术栈，截 1440px 和 390px 验收。
```

把 `home` 换成设计阶段实际产出的目录名。两个模型不在同一个客户端时，把交接目录交给实现模型即可。

**3. 有需要再做一轮审稿**

```text
/design-to-frontend review 对照样板和实现截图，列出最影响观感的三处差异，先不改代码。
```

这是工作流说明，不会自动切模型，也不需要配置新的 API。
