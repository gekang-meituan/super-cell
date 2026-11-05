# 快速上手

本文帮助你在几分钟内了解本仓库，并完成一次文档贡献流程。本仓库目前只包含文档，没有可运行的应用、依赖或测试套件。

## 仓库用途

`super-cell` 是用于验证 Super-agent 协作流程的实验仓库。它记录这条协作链路如何从需求触发、执行、提交、评审到合并，因此内容以说明文档为主，不承载业务代码。

## 克隆仓库

```bash
git clone https://github.com/gekang-meituan/super-cell.git
cd super-cell
```

## 文档结构

```text
super-cell/
├── README.md            # 仓库简介与文档入口
└── docs/
    └── quickstart.md    # 本文：快速上手与贡献流程
```

新增文档请放在 `docs/` 目录，并在 `README.md` 或相关文档中补充相对链接，便于他人发现。

## 一次贡献流程

1. **同步主分支并创建功能分支。** 分支名使用 `feature/` 前缀。

   ```bash
   git switch main
   git pull --ff-only
   git switch -c feature/update-quickstart
   ```

2. **修改或新增文档。** 编辑 `docs/` 下的 Markdown 文件；如果新增了文档，记得在 `README.md` 中添加指向它的相对链接。

3. **检查相对链接。** 提交前确认文档中引用的本地路径都真实存在。可以用下面的脚本逐个检查 Markdown 文件的 `.md` 相对链接：

   ```bash
   for file in README.md docs/*.md; do
     grep -oE '\]\([^)]+\.md\)' "$file" \
       | sed -E 's/^\]\(//; s/\)$//' \
       | while read -r link; do
           [ -e "$(dirname "$file")/$link" ] || echo "missing: $file -> $link"
         done
   done
   ```

   没有任何输出即表示这些相对链接都能在本地找到。

4. **提交并推送。**

   ```bash
   git add README.md docs
   git commit -m "docs: 更新快速上手文档"
   git push -u origin feature/update-quickstart
   ```

5. **创建 Pull Request。** 在 GitHub 上新建 PR，写明变更内容、实际做过的验证以及与相关 Issue 的关联，然后等待人工评审。

## 协作约定

- 不直接向 `main` 推送，所有改动通过 Pull Request 评审后由人工合并。
- 不开启自动合并，也不代替评审人批准或合并。
- 文档中只描述真实存在的目录、命令和验证结果，不编造应用、依赖或测试。
