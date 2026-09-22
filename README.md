# Personal Skills 仓库

存放我私人开发的 agent skill，用于在不同设备间同步同一套 skill。

## 目录结构

```
.
├── README.md
└── skills/
    └── <skill-name>/
        ├── SKILL.md      # 必填：skill 定义（含 name / description frontmatter）
        └── ...           # 可选：skill 引用的脚本、模板等辅助文件
```

## 新增一个 skill

1. 在 `skills/` 下新建以 skill 命名的目录。
2. 编写 `SKILL.md`，文件头部需包含 frontmatter：

   ```markdown
   ---
   name: my-skill
   description: 一句话说明这个 skill 做什么、何时使用。
   ---

   # 正文：skill 的具体指令与流程
   ```

3. 提交并推送：

   ```bash
   git add skills/my-skill
   git commit -m "feat: add my-skill skill"
   git push
   ```

## 在不同设备上使用

1. 克隆仓库：

   ```bash
   git clone <仓库地址> ~/skills-repo
   ```

2. 将 skill 目录软链（或复制）到 agent 的 skills 目录，例如：

   ```bash
   # pi / codex 的 skills 目录（按实际 agent 调整）
   ln -s ~/skills-repo/skills/my-skill ~/.agents/skills/my-skill
   ```

3. 更新设备上的 skill：

   ```bash
   cd ~/skills-repo && git pull
   ```

## 约定

- 每个 skill 独立一个目录，目录名与 frontmatter 中的 `name` 保持一致。
- SKILL.md 中引用相对路径时，以 skill 目录为基准。
- 不要把私密凭据、token 提交进仓库。
