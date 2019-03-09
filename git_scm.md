## Git 常用命令
```
q // git log 命令下等其他命令下推出查看 ctrl+c 也可以
```

```
git add // 添加到暂存区
```
如果是指定文件 git add xxx.js，如果是所有文件，git add .

// 取消暂存

```
git commit -m "initial project version" // 提交分支，但只存在本地分支，未推送到远程

// 在Linux系统中，commit信息使用单引号''包括，我使用的windows系统，信息应该是双引号""包括

git push // 推送到远程
```


- Changes to be committed 暂存状态，等待被提交
- Changes not staged for commit 已跟踪的文件内容发生了变化，但还没有放到暂存区
```
git status // 获取文件状态

// On branch master
// Your branch is ahead of 'origin/master' by 1 commit.
//   (use "git push" to publish your local commits)

git status --short // 状态简览 或 git status -s
```

```
git commit -a // 跳过暂存直接提交
```

```
git rm xx.xx // 删除指定文件（如果在暂存区或有进行修改会报错，可以进行强制删除）

git rm xx.xx -f // 强制删除
```

```
git mv file_from file_to // 文件重命名
```
其实，运行 git mv 就相当于运行了下面三条命令：
```
mv README.md README
git rm README.md
git add README

```

#### 提交历史

```
git log // 会按提交时间列出所有时间，最近的更新排在最上面

git log -p // 用来显示每次提交的内容差异，加上 -2 来仅显示最近两次提交

git log --stat // 每次提交的简略的统计信息

git log --pretty // 指定使用不同于默认方式的格式显示提交历史
git log --pretty=oneline // 单行显示
git log --pretty=format:"%h - %an, %ar : %s" // 定制要显示的记录格式 
```
Table 1. git log --pretty=format 常用的选项

选项 | 说明
--- | ---
%H    | 提交对象（commit）的完整哈希字串
%h    | 提交对象的简短哈希字串
%T    | 树对象（tree）的完整哈希字串
%t    | 树对象的简短哈希字串
%P    | 父对象（parent）的完整哈希字串
%p    | 父对象的简短哈希字串
%an   | 作者（author）的名字
%ae   | 作者的电子邮件地址
%ad   | 作者修订日期（可以用 --date= 选项定制格式）
%ar   | 作者修订日期，按多久以前的方式显示
%cn   | 提交者（committer）的名字
%ce   | 提交者的电子邮件地址
%cd   | 提交日期
%cr   | 提交日期，按多久以前的方式显示
%s    | 提交说明

Table 2. git log 的常用选项

选项 | 说明
--- | ---
-p              | 按补丁格式显示每个更新之间的差异。
--stat          | 显示每次更新的文件修改统计信息。
--shortstat     | 只显示 --stat 中最后的行数修改添加移除统计。
--name-only     | 仅在提交信息后显示已修改的文件清单。
--name-status   | 显示新增、修改、删除的文件清单。
--abbrev-commit | 仅显示 SHA-1 的前几个字符，而非所有的 40 个字符。
--relative-date | 使用较短的相对时间显示（比如，“2 weeks ago”）。
--graph         | 显示 ASCII 图形表示的分支合并历史。
--pretty        | 使用其他格式显示历史提交信息。可用的选项包括 oneline，short，full，fuller 和 format（后跟指定格式）。

```
git log --since=2.weeks // 两周内提交记录

```


Table 3. 限制 git log 输出的选项

选项 | 说明
--|--
-(n)                | 仅显示最近的 n 条提交
--since, --after    | 仅显示指定时间之后的提交。
--until, --before   | 仅显示指定时间之前的提交。
--author            | 仅显示指定作者相关的提交。
--committer         | 仅显示指定提交者相关的提交。
--grep              | 仅显示含指定关键字的提交
-S                  | 仅显示添加或移除了某个关键字的提交

