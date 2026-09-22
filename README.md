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

   > `description` 不能为空，否则 pi 会忽略该 skill。

3. 提交并推送：

   ```bash
   git add skills/my-skill
   git commit -m "feat: add my-skill skill"
   git push
   ```

## 让 pi 检测到 skill（一次性配置）

pi 只在**启动时**扫描 skill 目录并写入系统提示，对话中途无法热加载。因此需要提前告诉 pi 去哪里找本仓库的 skill——在全局设置 `~/.pi/agent/settings.json` 的 `skills` 数组里填上本仓库 `skills/` 目录的路径（即你 clone 仓库的位置）：

```json
{
  "skills": [
    "<本仓库路径>/skills"
  ]
}
```

配置一次后，每次启动 pi 都会自动扫描该目录，**无需软链，也无需每次跟 pi 说明**。

> 注意：修改 `settings.json` 后需**重启 pi** 才能生效（skill 列表在启动时确定）。

## 在不同设备上使用

1. clone 仓库：

   ```bash
   git clone <仓库地址>
   ```

2. 在新设备的 `~/.pi/agent/settings.json` 里，把 `skills` 数组填成该设备上的仓库路径：

   ```json
   { "skills": ["<本仓库路径>/skills"] }
   ```

3. 重启 pi，skill 即出现在列表中。

4. 更新设备上的 skill：

   ```bash
   cd <本仓库路径> && git pull
   ```

   `git pull` 后再重启 pi，即可加载新 skill。

## 约定

- 每个 skill 独立一个目录，目录名与 frontmatter 中的 `name` 保持一致。
- SKILL.md 中引用相对路径时，以 skill 目录为基准。
- 不要把私密凭据、token 提交进仓库。
