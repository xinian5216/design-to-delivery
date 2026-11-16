# design-to-delivery

先把方案写成可验收的基准，再交给编码模型实现。适用于前端、后端 API、插件 / 扩展、CLI、SDK、自动化和游戏功能，也可用于现有项目的重构或集成。

原来的「Opus 定稿、Gemini 实现、Opus 复核」仍然能用。模型可替换，也可以由同一个模型完成。这个 Skill 不会自动切模型，不需要接新 API。

| 阶段 | 做什么 | 交什么 |
| --- | --- | --- |
| `design` | 定范围、关键决策和验收条件，不改产品代码 | 交接说明及必要的原型、接口样例或测试用例 |
| `implement` | 按基准实现，先跑通一条主路径 | 可运行的改动，以及实际执行的检查结果 |
| `review` | 对照基准验收，默认不改代码 | 按影响排序的偏差、复现方法与未验证项 |

同一套流程，不同项目只换验收依据。前端用参考样板和同条件截图，API 用契约和测试，插件用目标宿主里的实测。小改动用几条验收条件就够。跨模型或复杂任务没有既定交接目录时，用 `handoff/<task>/handoff.md`，再附上基准样例。

## 安装到 Antigravity

打开 [SKILL.md](./SKILL.md)，用 **Raw** 保存为 `SKILL.md`，放进项目的 `.agents/skills/design-to-delivery/` 目录。仓库仍只需要这一个文件。

```text
your-project/
└── .agents/
    └── skills/
        └── design-to-delivery/
            └── SKILL.md
```

想在 Antigravity App 的多个项目中使用，可以放到 `~/.gemini/config/skills/design-to-delivery/SKILL.md`。其他客户端请使用各自的技能目录。不同版本的目录约定见 [Antigravity 官方说明](https://antigravity.google/docs/skills)。

**从旧版迁移**：仓库已更名为 [`design-to-delivery`](https://github.com/xinian5216/design-to-delivery)。用新版替换旧文件，把本地技能目录从 `design-to-frontend` 改为 `design-to-delivery`，之后用 `/design-to-delivery` 调用。阶段名称不变，已有的 `design-handoff/` 交接文件可以继续用。

## 示例

**浏览器扩展｜设计、实现、验收**

```text
/design-to-delivery design 设计一个标签页分组扩展。先定 MVP、Chrome 版本、所需权限，以及权限被拒时的行为。交付方案，先别写产品代码。
```

```text
/design-to-delivery implement 读取 handoff/tab-groups/handoff.md，按方案实现，并记录目标浏览器的安装与关键路径检查结果。
```

```text
/design-to-delivery review 对照交接说明检查扩展，重点看权限申请、拒绝后能否继续使用，以及重启后能否恢复分组。只报告问题。
```

`tab-groups` 换成实际生成的任务目录名。跨客户端时，把交接目录和下一阶段提示一起交给实现模型。

**后端 API｜做到成品**

```text
/design-to-delivery 给现有订单 API 加幂等提交。保留现有接口，先定重复请求和冲突时的响应，再实现并验证不会创建第二条订单。
```

**前端｜继续沿用旧交接物**

```text
/design-to-delivery implement 读取 design-handoff/home/handoff.md，按样板实现首页，保留现有技术栈，并用桌面与移动端截图验收。
```
