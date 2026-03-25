
# Git 命令速查清单

## 1. 配置 (Configuration)

| 命令 | 说明 |
| :--- | :--- |
| `git config --global user.name "name"` | 设置全局用户名 |
| `git config --global user.email "email"` | 设置全局邮箱 |
| `git config --list` | 查看当前所有配置 |
| `git config --global alias.<alias> <cmd>` | 设置命令别名（如 `git config --global alias.co checkout`） |

## 2. 初始化与获取 (Init & Clone)

| 命令 | 说明 |
| :--- | :--- |
| `git init` | 在当前目录初始化一个新的 Git 仓库 |
| `git clone <url>` | 克隆远程仓库到本地 |
| `git clone -b <branch> <url>` | 克隆远程仓库的指定分支 |

## 3. 远程仓库管理 (Remote)

> [!info] `git clone`其实内部执行了`git remote add origin <url>`, `git pull`和`git push`默认是origin。可以添加多个远程仓库。
> 

| 命令 | 说明 |
| :--- | :--- |
| `git remote -v` | 查看所有远程仓库地址 |
| `git remote add origin <url>` | 添加远程仓库关联（通常命名为 origin） |
| `git remote set-url origin <new_url>` | 修改远程仓库地址 |
| `git remote remove origin` | 删除远程仓库关联 |
| `git remote rename <old> <new>` | 重命名远程仓库引用 |

## 4. 提交与修改 (Stage & Commit)

| 命令 | 说明 |
| :--- | :--- |
| `git status` | 查看当前工作区状态（变更文件列表） |
| `git add .` | 将当前目录所有变更添加到暂存区 |
| `git add <file>` | 将指定文件添加到暂存区 |
| `git commit -m "msg"` | 提交暂存区内容到本地仓库 |
| `git commit --amend` | 修改最近一次提交的说明（或追加文件到上次提交） |
| `git diff` | 查看工作区与暂存区的差异 |
| `git diff --staged` | 查看暂存区与最后一次提交的差异 |

## 5. 分支管理 (Branching)

> [!info] 分支是代码仓库中的**独立开发线**。在 Git 中，分支本质上是一个指向某个具体提交（Commit）的轻量级可移动指针。
> **隔离性**：允许在不影响主代码（通常是 `main` 或 `master`）的情况下进行新功能开发或 Bug 修复。
> **并行开发**：团队成员可以同时在不同的分支上工作，互不干扰。

| 命令 | 说明 |
| :--- | :--- |
| `git branch` | 列出本地所有分支 |
| `git branch -a` | 列出本地和远程所有分支 |
| `git branch <name>` | 创建新分支（但不切换） |
| `git checkout -b <name>` | 创建并切换到新分支 |
| `git switch -c <name>` | 创建并切换到新分支（新版命令） |
| `git checkout <name>` | 切换分支 |
| `git switch <name>` | 切换分支（新版命令） |
| `git merge <branch>` | 将指定分支合并到当前分支 |
| `git branch -d <name>` | 删除本地分支（需已合并） |
| `git branch -D <name>` | 强制删除本地分支（无论是否合并） |
| `git branch -m <old> <new>` | 重命名本地分支 |

## 6. 远程同步 (Sync)

| 命令 | 说明 |
| :--- | :--- |
| `git fetch` | 拉取远程更新但不合并 |
| `git pull <remote> <branch>` | 拉取远程更新并合并到当前分支 |
| `git push <remote> <branch>` | 推送本地修改到远程仓库 |
| `git push -u origin <branch>` | 推送并设置上游关联（首次推送时使用） |
| `git push --force` | 强制推送到远程（慎用，会覆盖远程历史） |
| `git push origin --delete <branch>` | 删除远程分支 |

## 7. 撤销与回退 (Undo & Reset)

| 命令 | 说明 |
| :--- | :--- |
| `git checkout -- <file>` | 丢弃工作区指定文件的修改（恢复到最近一次 commit） |
| `git restore <file>` | 丢弃工作区指定文件的修改（新版命令） |
| `git reset HEAD <file>` | 将文件从暂存区移出（取消 add） |
| `git restore --staged <file>` | 将文件从暂存区移出（新版命令） |
| `git reset --soft HEAD^` | 撤销最近一次 commit，保留代码在暂存区 |
| `git reset --mixed HEAD^` | 撤销最近一次 commit，保留代码在工作区（默认模式） |
| `git reset --hard HEAD^` | 撤销最近一次 commit，**删除**所有代码修改 |
| `git reset --hard <commit_id>` | 强制回退到指定版本 |

## 8. 储藏与清理 (Stash & Clean)

| 命令 | 说明 |
| :--- | :--- |
| `git stash` | 暂时储藏当前工作区修改 |
| `git stash save "msg"` | 储藏并添加备注 |
| `git stash list` | 查看储藏列表 |
| `git stash pop` | 恢复最近一次储藏并从列表中删除 |
| `git stash apply` | 恢复最近一次储藏但不删除 |
| `git stash drop` | 删除最近一次储藏 |
| `git clean -fd` | 强制删除工作区中未追踪（Untracked）的文件和目录 |

## 9. 查看日志与排错 (Log & Blame)

| 命令 | 说明 |
| :--- | :--- |
| `git log` | 查看提交历史 |
| `git log --oneline --graph` | 以图形化简略方式查看提交历史 |
| `git blame <file>` | 查看文件每一行的最后修改人（溯源） |
| `git reflog` | 查看 HEAD 的移动记录（找回丢失的 commit 救命命令） |
| `git cherry-pick <commit_id>` | 将其他分支的某次提交应用到当前分支 |

## 10. 标签管理 (Tag)

| 命令 | 说明 |
| :--- | :--- |
| `git tag` | 列出所有标签 |
| `git tag <name>` | 在当前 commit 打标签 |
| `git tag -a <name> -m "msg"` | 创建附注标签 |
| `git push origin <tagname>` | 推送指定标签到远程 |
| `git push origin --tags` | 推送所有标签到远程 |
| `git tag -d <name>` | 删除本地标签 |
| `git push origin :refs/tags/<name>` | 删除远程标签 |