---
name: aab-git-workflow
description: AAB 的 Git 工作流——最小化版本控制习惯。用于任何需要 git 操作的场景：提交代码、回退、分支管理、备份。也用于用户提到"提交""commit""push""备份一下""保存版本"时。规则极简，因为 AAB 大部分是个人项目。
---

# Git Workflow — AAB 极简版

## 核心原则

AAB 的项目 90% 是个人项目，不需要 PR/Code Review/CI 那套。

只需要三条规则：
1. **做了能跑的东西就 commit**
2. **commit message 用中文，说清楚改了啥**
3. **答辩/展示前 push 到远程（备份）**

## 提交时机

```
改完一个功能 → commit
改完一个页面 → commit
Demo 能跑了 → commit
每天结束前 → commit
答辩前一晚 → commit + push
```

不需要等到"完美"才 commit。commit 是保存点，不是发布。

## Commit Message 格式

```
[类型] 简短描述

类型：
  feat:     新功能
  fix:      修 bug
  style:    调样式
  refactor: 重构（不改功能）
  data:     改数据
  cleanup:  清理代码
  backup:   答辩前备份
```

示例：
```
feat: 添加数据看板页面
fix: 修复移动端卡片溢出
style: 调整暗色主题对比度
data: 更新示例数据
backup: 三创赛答辩前备份
```

不需要英文、不需要 Conventional Commits、不需要 scope。怎么快怎么来。

## 日常命令

```bash
# 看改了啥
git status
git diff --stat

# 提交全部改动
git add .
git commit -m "feat: 添加xxx"

# 推到 GitHub（备份）
git push

# 回退（没 push 过）
git reset --hard HEAD~1    # 撤销最近一次 commit
git checkout -- <file>     # 撤销单个文件的改动

# 看历史
git log --oneline -10
```

## 分支策略

```
个人项目：在 main 上直接改（不用分支）
比赛项目：答辩前从 main 拉一个 release 分支，只修 bug 不加功能
协作项目：每人一个分支，合并前让对方看一眼
```

不需要 feature branch / develop / staging 那套。一个人没必要。

## 答辩前备份流程

```bash
# 1. 确认所有改动已提交
git status  # 应该是 clean

# 2. 推送到 GitHub
git push origin main

# 3. 额外备份一份到 U 盘
# 或者直接拷走整个项目文件夹

# 4. 打 tag 标记版本
git tag v1.0-demo
git push origin v1.0-demo
```

## 不需要的

- Conventional Commits（`feat(scope):`）—— AAB 不需要 scope
- Husky / lint-staged —— 个人项目不需要 pre-commit hook
- CI/CD Pipeline —— 单文件 HTML 不需要
- Squash merge / rebase —— 个人项目直接 commit，不用纠结历史
