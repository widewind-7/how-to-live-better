# Hermes Agent 版「人生决策」技能（life-decision-guide）

让 Hermes Agent 照《高性价比人生指南》回答具体问题：该不该做、值不值、怎么选、出事了先做什么、能领哪笔钱、这样犯不犯法。

规则来自上游 [eternity4719/HowToLiveBetter](https://github.com/eternity4719/HowToLiveBetter) 的
[`skills/life-decision-guide`](https://github.com/eternity4719/HowToLiveBetter/blob/main/skills/life-decision-guide)
（MIT）。上游那份给 Claude Code 和 Codex 用；这一份是给 **Hermes Agent** 用的移植版，规则一字未改，
只改了取数方式和安装位置。

## 装到 Hermes

把 `life-decision-guide` 整个目录复制到 Hermes 的 skills 目录：

```bash
# Windows 默认路径
mkdir -p "C:/Users/<你的用户名>/AppData/Local/hermes/skills/life-decision-guide"
cp hermes-skill/life-decision-guide/SKILL.md \
   "C:/Users/<你的用户名>/AppData/Local/hermes/skills/life-decision-guide/SKILL.md"
```

装完重启 Hermes（或在设置里重载技能）。之后提到「人生指南」，或问「替朋友担保签不签」「每天通勤两小时值不值」
这类问题，就会自动命中；也可以显式说「用 life-decision-guide 回答」。

## 正文从哪来

技能**不存正文**，每次现读，所以书更新了技能也不会过时。首选本地正本，先克隆一份：

```bash
mkdir -p "C:/Users/<你的用户名>/AppData/Local/hermes/books"
git clone --depth 1 https://github.com/eternity4719/HowToLiveBetter.git \
  "C:/Users/<你的用户名>/AppData/Local/hermes/books/HowToLiveBetter"
```

没有这个目录时，技能会退回到临时克隆，功能不受影响。每次使用前技能会先 `git pull --ff-only` 拉最新。

## 跟上游那份的区别

| | 上游版（Claude Code / Codex） | 这份（Hermes） |
|---|---|---|
| 取正文 | 本地没有就克隆到临时目录 | 指向固定的本地正本，每次先 `git pull` |
| 检索 | 假设有 Grep/Read，或手写 `grep -rn` / `sed` | 用 Hermes 的 `search_files` / `read_file` |
| 安装位置 | `~/.claude/skills/` 或 `~/.agents/skills/` | `~/AppData/Local/hermes/skills/` |

规则本身（第 0 步急症/自杀/法律程序优先、四类口径不互相折算、受益分四档、法律条目必须写过程成本、
数字照抄不加料、查不到就说查不到）**与上游完全一致**。

## 授权

正文是 CC BY 4.0，上游的 skill 和代码是 MIT。本目录沿用 MIT，规则移植自上游并在此注明出处。
