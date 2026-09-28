# Git 每日实战训练手册

> 适用目录：`D:\Ops_study`  
> 建议文件名：`Git_Practice.md`  
> 目标：通过每日 15～30 分钟的滚动实战，把 Git 从“记命令”练成“看到场景就知道怎么处理”。

---

# 1. 使用原则

这份手册不是 Git 命令大全，而是训练手册。

每天训练固定分成三部分：

1. **旧知识回忆**：不看笔记，先凭记忆完成昨天或前几天的操作。
2. **当天新内容**：只增加少量新命令或新概念。
3. **场景实战**：主动制造一个问题，再用 Git 解决。

推荐每天训练 15～30 分钟。

核心方法：

- **Retrieval Practice（检索练习）**：先回忆，再查答案。
- **Spaced Repetition（间隔重复）**：旧命令不断重新出现。
- **Deliberate Practice（刻意练习）**：主动制造错误、冲突和恢复场景。

不要追求“今天学了多少命令”，而要追求：

> 我能否判断当前 Git 状态，并知道下一步该做什么。

---

# 2. 当前练习环境

你的长期 Git 实验仓库：

```text
D:\Ops_study
```

当前已有：

```text
README.txt
```

并已经同步到 GitHub。

建议以后目录逐渐变成：

```text
D:\Ops_study
│
├─ README.txt
├─ Git_Practice.md
├─ Git_Notes.md
├─ linux\
├─ scripts\
├─ database\
└─ lab\
```

其中：

- `Git_Practice.md`：长期训练手册
- `Git_Notes.md`：只记录你真正踩过的坑
- `lab\`：专门制造 Git 实验、冲突、错误恢复

---

# 3. 每天开始前的固定动作

每天打开 PowerShell 后：

```powershell
cd D:\Ops_study
git status
git log --oneline --decorate -5
```

先回答三个问题：

1. 我现在在哪个分支？
2. 工作区是否有修改？
3. 最近几次 commit 是什么？

建议养成一个长期习惯：

> **先 `status`，再动手。**

Git 出问题时，也优先执行：

```powershell
git status
```

---

# 4. Git 最核心的心智模型

先牢牢记住三个区域：

```text
Working Directory
    工作区

    │ git add
    ▼

Staging Area
    暂存区

    │ git commit
    ▼

Repository
    本地仓库
```

再加上 GitHub：

```text
Working Directory
        │
        ▼
Staging Area
        │
        ▼
Local Repository
        │
        │ git push
        ▼
Remote Repository
       GitHub
```

很多 Git 命令，本质上都是在这些区域之间移动内容。

---

# 5. 30 天训练计划

---

## Day 1：重新建立最基本工作流

### 目标

熟练：

```text
git status
git add
git commit
git log
```

### 实战

创建文件：

```powershell
echo "Git Day 1" > lab_day1.txt
```

观察：

```powershell
git status
```

加入暂存区：

```powershell
git add lab_day1.txt
git status
```

提交：

```powershell
git commit -m "practice: Git day 1 basic workflow"
```

查看历史：

```powershell
git log --oneline
```

### 今天必须理解

```text
Untracked
→ Staged
→ Committed
```

### 自测

不看笔记完成：

```text
创建文件 → add → commit → 查看历史
```

---

## Day 2：理解 diff

### 复习

不看笔记完成一次：

```text
修改文件 → status → add → commit
```

### 新内容

```powershell
git diff
git diff --staged
```

### 实战

修改：

```powershell
echo "second line" >> lab_day1.txt
```

执行：

```powershell
git diff
```

然后：

```powershell
git add lab_day1.txt
git diff
git diff --staged
```

### 核心理解

```text
git diff
```

主要看：

> 工作区 vs 暂存区

而：

```text
git diff --staged
```

主要看：

> 暂存区 vs HEAD

---

## Day 3：撤销尚未暂存的修改

### 新内容

```powershell
git restore <file>
```

### 场景

故意修改：

```powershell
echo "wrong content" >> README.txt
```

检查：

```powershell
git diff
```

假装你发现：

> 我改错了，而且还没 add。

恢复：

```powershell
git restore README.txt
```

再次：

```powershell
git status
git diff
```

### 今日目标

看到：

> 文件修改了，但没 add，我不要这些修改了。

自然想到：

```text
git restore
```

---

## Day 4：撤销暂存

### 新内容

```powershell
git restore --staged <file>
```

### 场景

```powershell
echo "temporary change" >> README.txt
git add README.txt
```

现在假设：

> 我不应该把 README.txt 放进下一次 commit。

执行：

```powershell
git restore --staged README.txt
```

观察：

```powershell
git status
```

注意：

> `restore --staged` 只是撤销 add，不删除工作区修改。

---

## Day 5：综合工作区与暂存区

今天原则上不学新命令。

### 综合题

自己完成：

1. 修改 `README.txt`
2. 创建 `day5.txt`
3. `git status`
4. 只 add `day5.txt`
5. 查看 `git diff`
6. 查看 `git diff --staged`
7. 把 `day5.txt` 从暂存区移出
8. 重新 add
9. commit
10. 查看 log

### 要求

尽量不看答案。

---

## Day 6：文件删除与重命名

### 新内容

```powershell
git rm
git mv
```

### 实战

创建：

```powershell
echo "rename test" > old_name.txt
git add old_name.txt
git commit -m "practice: add rename test file"
```

重命名：

```powershell
git mv old_name.txt new_name.txt
git status
git commit -m "practice: rename file"
```

删除：

```powershell
git rm new_name.txt
git status
git commit -m "practice: remove test file"
```

---

## Day 7：第一周综合考试

今天不学新命令。

### 要求独立完成

1. 创建两个文件
2. 查看状态
3. 修改其中一个
4. 查看差异
5. 暂存两个文件
6. 查看 staged diff
7. 撤销其中一个文件的暂存
8. 提交剩余文件
9. 恢复另一个文件的错误修改
10. 查看最近 5 条提交

### 第一周应熟练

```text
status
add
commit
log
diff
diff --staged
restore
restore --staged
rm
mv
```

---

# 第二阶段：分支

---

## Day 8：认识 branch

### 新内容

```powershell
git branch
git switch
git switch -c
```

查看：

```powershell
git branch
```

创建并切换：

```powershell
git switch -c dev
```

查看：

```powershell
git branch
```

回到主分支：

```powershell
git switch main
```

如果你的默认主分支叫 `master`，则使用：

```powershell
git switch master
```

---

## Day 9：在不同分支独立提交

创建：

```powershell
git switch -c feature/day9
echo "feature branch" > feature_day9.txt
git add feature_day9.txt
git commit -m "practice: add day9 feature"
```

回主分支：

```powershell
git switch main
```

观察：

```powershell
dir
git log --oneline --all --decorate --graph
```

### 今日理解

分支不是“复制一个文件夹”。

Git 分支本质上可以理解为：

> 一个指向某次 commit 的可移动指针。

---

## Day 10：merge

### 新内容

```powershell
git merge
```

从主分支合并：

```powershell
git switch main
git merge feature/day9
```

查看：

```powershell
git log --oneline --graph --decorate --all
```

---

## Day 11：删除分支

### 新内容

```powershell
git branch -d <branch>
```

已经合并后：

```powershell
git branch -d feature/day9
```

理解：

```text
-d
```

是相对安全的删除方式。

不要急着大量使用：

```text
-D
```

---

## Day 12：制造第一次 merge conflict

创建：

```powershell
echo "original" > conflict.txt
git add conflict.txt
git commit -m "practice: prepare conflict file"
```

创建分支：

```powershell
git switch -c conflict-test
```

修改：

```powershell
echo "change from branch" > conflict.txt
git add conflict.txt
git commit -m "practice: branch conflict change"
```

回主分支：

```powershell
git switch main
echo "change from main" > conflict.txt
git add conflict.txt
git commit -m "practice: main conflict change"
```

合并：

```powershell
git merge conflict-test
```

此时应该出现冲突。

打开文件会看到类似：

```text
<<<<<<< HEAD
change from main
=======
change from branch
>>>>>>> conflict-test
```

手工修改成最终内容，然后：

```powershell
git add conflict.txt
git commit
```

---

## Day 13：再次制造冲突

重复 Day 12。

目标不是学习新东西，而是让：

```text
CONFLICT
```

从“吓人”变成普通工作状态。

---

## Day 14：第二周综合考试

独立完成：

1. 创建分支
2. 分支中提交
3. 主分支中提交
4. merge
5. 制造冲突
6. 解决冲突
7. 删除已合并分支
8. 使用 graph 查看历史

重点命令：

```powershell
git log --oneline --graph --decorate --all
```

---

# 第三阶段：GitHub 与远程仓库

---

## Day 15：理解 remote

### 新内容

```powershell
git remote -v
```

执行：

```powershell
git remote -v
```

理解：

```text
origin
```

通常只是远程仓库的默认别名。

---

## Day 16：push

### 复习

做一个新 commit。

然后：

```powershell
git push
```

如果新分支第一次推送：

```powershell
git push -u origin <branch-name>
```

理解：

```text
-u
```

建立 upstream tracking relationship。

---

## Day 17：fetch

### 新内容

```powershell
git fetch
```

执行：

```powershell
git fetch
```

然后查看：

```powershell
git branch -a
git log --oneline --all --graph --decorate
```

### 核心理解

`fetch`：

> 更新你对远程仓库状态的认知，但默认不会直接修改当前工作分支。

---

## Day 18：pull

### 新内容

```powershell
git pull
```

理解：

```text
pull ≈ fetch + integrate
```

具体整合行为受配置影响，常见是 merge 或 rebase。

不要只记：

> pull = 下载。

---

## Day 19：本地分支与远程跟踪分支

观察：

```powershell
git branch -vv
git branch -a
```

理解：

```text
main
origin/main
```

不是同一个东西。

---

## Day 20：模拟 GitHub 修改

在 GitHub 网页修改一个小文件并 commit。

回本地：

```powershell
git fetch
git status
git log --oneline --all --graph --decorate
```

观察远端变化。

然后再：

```powershell
git pull
```

---

## Day 21：第三周综合考试

自己完成：

1. 本地创建分支
2. commit
3. push
4. GitHub 页面修改
5. 本地 fetch
6. 查看远端变化
7. pull
8. 查看 log graph

---

# 第四阶段：撤销、恢复与“后悔药”

---

## Day 22：修改最后一次 commit

### 新内容

```powershell
git commit --amend
```

先 commit：

```powershell
echo "amend test" > amend.txt
git add amend.txt
git commit -m "wrong message"
```

修改最后一次提交信息：

```powershell
git commit --amend -m "practice: correct commit message"
```

注意：

> amend 会生成新的 commit。

已经 push 的公共提交不要随便 amend。

---

## Day 23：reset 三种模式

### 新内容

```text
git reset --soft
git reset --mixed
git reset --hard
```

先理解，不急着背。

大致可以这样记：

```text
--soft
只移动 HEAD

--mixed
移动 HEAD + 重置暂存区

--hard
移动 HEAD + 重置暂存区 + 工作区
```

### 安全要求

今天所有 reset 实验只在专门练习分支完成。

```powershell
git switch -c reset-lab
```

---

## Day 24：revert

### 新内容

```powershell
git revert <commit>
```

理解 reset 与 revert 的核心区别：

```text
reset
移动历史指针

revert
新增一个“反向修改”的 commit
```

公共历史里通常更偏向使用 revert。

---

## Day 25：reflog —— 救命命令

### 新内容

```powershell
git reflog
```

制造几个实验提交，然后在练习分支：

```powershell
git reset --hard HEAD~2
```

查看：

```powershell
git log --oneline
```

两个 commit 看起来消失。

再：

```powershell
git reflog
```

找到原来的 commit。

可以用：

```powershell
git reset --hard <commit-id>
```

恢复。

### 今日重点

真正理解：

> Git 中很多“误删除提交”并没有立刻彻底消失。

---

## Day 26：stash

### 新内容

```powershell
git stash
git stash list
git stash pop
```

场景：

> 工作做到一半，突然要切分支修 bug，但当前内容还不适合 commit。

实验：

```powershell
echo "unfinished work" >> README.txt
git stash
git status
git stash list
git stash pop
```

---

## Day 27：cherry-pick

### 新内容

```powershell
git cherry-pick <commit>
```

理解场景：

> 我只想把另一个分支里的某一个 commit 拿过来，而不是合并整个分支。

创建实验分支并做两个 commit，然后在主分支 cherry-pick 其中一个。

---

## Day 28：rebase 基础

### 新内容

```powershell
git rebase
```

今天重点是理解，不追求复杂操作。

对比：

```text
merge
保留真实分叉结构

rebase
重新整理提交基线，使历史更线性
```

重要原则：

> 不要随意 rebase 已经共享给其他人的公共提交历史。

---

## Day 29：交互式 rebase

### 新内容

```powershell
git rebase -i HEAD~3
```

认识：

```text
pick
reword
squash
fixup
drop
```

只在实验分支操作。

目标：

- 修改 commit message
- 合并几个小 commit

---

## Day 30：综合故障演练

今天不学新命令。

完成以下场景：

### 场景 1

文件改错但没 add。

你应该想到：

```text
restore
```

### 场景 2

错误文件已经 add，但没 commit。

想到：

```text
restore --staged
```

### 场景 3

最后一次 commit message 写错。

想到：

```text
commit --amend
```

### 场景 4

公共历史中的错误 commit 需要撤销。

想到：

```text
revert
```

### 场景 5

误 reset 后提交“消失”。

想到：

```text
reflog
```

### 场景 6

当前工作做到一半，但必须紧急切分支。

想到：

```text
stash
```

### 场景 7

只需要另一个分支的一次 commit。

想到：

```text
cherry-pick
```

### 场景 8

两个分支修改同一位置。

想到：

```text
merge conflict
```

并独立解决。

---

# 6. 30 天以后怎么继续

30 天不是结束。

从第 31 天起采用：

```text
真实使用 + 随机故障训练
```

每周至少做一次综合 Git 实验。

推荐随机抽取这些场景：

1. 修改未暂存，需要撤销
2. 错误 add
3. 错误 commit
4. 错误 commit message
5. merge conflict
6. pull 冲突
7. reset 后恢复
8. stash 临时工作
9. cherry-pick
10. rebase
11. 删除分支
12. 新建远程分支
13. 本地落后于 GitHub
14. 本地领先于 GitHub
15. 本地和 GitHub 分叉

---

# 7. 建议长期形成的 Git 操作习惯

## 习惯 1：操作前先 status

```powershell
git status
```

---

## 习惯 2：commit 前看 diff

至少经常使用：

```powershell
git diff
git diff --staged
```

不要盲目：

```powershell
git add .
git commit
```

---

## 习惯 3：commit 尽量小而清晰

避免一个 commit 同时包含：

```text
修 bug
改文档
重构
加新功能
删除测试代码
```

更好的提交应该是逻辑单一的。

---

## 习惯 4：commit message 说明“为什么改”

例如：

```text
practice: add Git restore exercise
fix: correct path parsing on Windows
docs: update Linux notes
```

---

## 习惯 5：破坏性命令前先确认状态

特别是：

```powershell
git reset --hard
git clean
git branch -D
```

执行前至少：

```powershell
git status
git log --oneline -5
```

练习阶段只在实验分支使用。

---

# 8. Git 命令能力地图

## Level 1：日常基础

```text
status
add
commit
log
diff
restore
```

---

## Level 2：分支开发

```text
branch
switch
merge
branch -d
```

---

## Level 3：远程协作

```text
remote
fetch
pull
push
branch -vv
```

---

## Level 4：错误恢复

```text
commit --amend
reset
revert
reflog
stash
```

---

## Level 5：历史整理

```text
cherry-pick
rebase
rebase -i
```

---

## Level 6：进阶工具

后续继续学习：

```text
git tag
git blame
git bisect
git clean
git worktree
git hooks
git submodule
```

---

# 9. 高频命令速查表

| 场景 | 命令 |
|---|---|
| 看当前状态 | `git status` |
| 看未暂存修改 | `git diff` |
| 看已暂存修改 | `git diff --staged` |
| 加入暂存区 | `git add <file>` |
| 提交 | `git commit -m "message"` |
| 看简洁历史 | `git log --oneline` |
| 看分支图 | `git log --oneline --graph --decorate --all` |
| 撤销未暂存修改 | `git restore <file>` |
| 撤销 add | `git restore --staged <file>` |
| 创建并切换分支 | `git switch -c <branch>` |
| 切换分支 | `git switch <branch>` |
| 合并分支 | `git merge <branch>` |
| 查看远程仓库 | `git remote -v` |
| 下载远程信息 | `git fetch` |
| 拉取并整合 | `git pull` |
| 推送 | `git push` |
| 临时保存工作 | `git stash` |
| 恢复 stash | `git stash pop` |
| 修改最后一次提交 | `git commit --amend` |
| 安全撤销某次公共提交 | `git revert <commit>` |
| 查看 HEAD 操作历史 | `git reflog` |
| 拿某一个 commit | `git cherry-pick <commit>` |

---

# 10. Git 故障排查顺序

以后遇到 Git 问题，不要立刻乱输命令。

优先按这个顺序：

```text
1. git status
2. git branch
3. git log --oneline --graph --decorate --all
4. git diff
5. git diff --staged
6. git reflog
```

然后回答：

```text
我在哪个分支？

工作区发生了什么？

暂存区有什么？

HEAD 在哪？

本地和远程谁领先？

我要保留哪些修改？

我要丢弃哪些修改？
```

想清楚以后再操作。

---

# 11. Git_Notes.md 应该记录什么

不要把教程全部抄进去。

只记录：

```text
我真正遇到过的问题
+
问题原因
+
解决方法
+
以后如何判断
```

例如：

```markdown
## 误把 README.txt add 进暂存区

现象：

git status 显示：

Changes to be committed

但我暂时不想提交 README.txt。

解决：

git restore --staged README.txt

注意：

这个命令不会删除 README.txt 的工作区修改。
```

这种笔记以后最有价值。

---

# 12. 每日训练记录模板

每天练完，可以在本文件底部追加：

```markdown
## 2026-XX-XX Git Practice

今天练习：

- git status
- git diff
- git restore

今天卡住：

- 一开始分不清 restore 和 restore --staged

今天已经能独立完成：

- 撤销未 add 的修改

明天复习：

- restore
- restore --staged
```

不要写成长篇学习总结。

只记录真正容易忘的点。

---

# 13. 判断自己是否“学会 Git”的标准

不是：

> 我能背多少 Git 命令。

而是看到这些情况时能自然做出判断：

```text
文件改错了
→ 判断是否已经 add

commit 错了
→ 判断是否已经 push

分支冲突
→ 判断冲突文件和最终内容

远程有更新
→ 判断 fetch / pull

提交消失
→ 想到 reflog

临时切任务
→ 想到 stash

只想拿一个提交
→ 想到 cherry-pick
```

真正熟练以后，你首先想到的往往不是命令，而是：

> **Git 当前状态是什么？**

然后命令自然就出来了。

---

# 14. 最终目标

对于运维、开发和日常技术工作而言，能够熟练掌握下面这些能力，已经足以覆盖绝大多数 Git 使用：

```text
提交
查看差异
撤销
分支
合并
解决冲突
远程同步
stash
reset / revert
reflog 恢复
cherry-pick
rebase
```

你不需要一开始就追求掌握 Git 的所有底层实现。

先让 Git 成为每天都在使用的工具。

长期目标：

> 从“我记得有一个 Git 命令能做这个”
>
> 变成
>
> “我知道现在 Git 处于什么状态，也知道怎样安全地把它变成目标状态。”
