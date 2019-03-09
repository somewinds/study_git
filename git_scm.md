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

git log --oneline // 单行显示历史

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

### 撤消操作

```
git commit --amend // ??? 如果自上次提交以来你还未做任何修改（例如，在上次提交后马上执行了此命令），那么快照会保持不变，而你所修改的只是提交信息。

git reset * // 撤销所有暂存文件
git reset xx.xxx // 撤销单个文件

git checkout * // 丢弃所有文件的修改，无法丢弃暂存区内的文件的修改
git checkout -- xx.xxx // 丢弃单个文件的修改，或 git checkout xx.xxx
```

### 2.5 远程仓库的使用
```
git remote -v // 会显示需要读写远程仓库使用的 Git 保存的简写与其对应的 URL

git remote show origin // 查看远程仓库的更多信息

git remote rename pb paul // 重命名远程参考的简写名
```

### 2.6 打标签

```
git tag // 列出所有标签

git tag -a v1.4 -m "第一条标签" // -m 选项指定了一条将会存储在标签中的信息

git show v1.4 // 可以看到标签信息与对应的提交信息

git tag v1.5 // 轻量标签创建，在此标签上运行 git show，你不会看到额外的标签信息，命令只会显示出提交信息

git tag -a 标签-文件重命名 500815ed0df1a1477920c3196f454e5fb80dfb3a // 为指定提交添加标签

git push origin [tagname] // 在创建完标签后你必须显式地推送标签到共享服务器上

git tag -d [tagname] // 删除本地仓库的指定标签

git push <remote> :refs/tags/v1.4 // 删除远程仓库的标签，注意分号
```

进入vim编辑器后，INSERT 进入编辑模式，在第一行空行输入标签备注信息，ESC 退出编辑模式，英文输入 :wq 保存并退出编辑器

### 2.7 Git 别名

```
git config --global alias.ci commit // 设置git命令 commit 的别名
git config --global alias.st status // 设置git命令 status 的别名
git config --global alias:ll "log --pretty=oneline" // 设置git命令 log --pretty=oneline 的别名

git config --global --unset alias.ll // 删除已设置的 ll 别名

git config --global --replace-all alias.ll log // 将别名重置为新的别名指令

```

重复添加会提示：
```
warning: alias.ll has multiple values
error: cannot overwrite multiple values with a single value
       Use a regexp, --add or --replace-all to change alias.ll.
```

## 三、Git 分支
在很多版本控制系统中，这是一个略微低效的过程——常常需要完全创建一个源代码目录的副本。对于大项目来说，这样的过程会耗费很多时间。

有人把 Git 的分支模型称为它的`‘必杀技特性’'，也正因为这一特性，使得 Git 从众多版本控制系统中脱颖而出。 

Git 处理分支的方式可谓是难以置信的轻量，创建新分支这一操作几乎能在瞬间完成，并且在不同分支之间的切换操作也是一样便捷。

与许多其它版本控制系统不同，Git 鼓励在工作流程中频繁地使用分支与合并，哪怕一天之内进行许多次。

理解和精通这一特性，你便会意识到 Git 是如此的强大而又独特，并且从此真正改变你的开发方式。

![image](https://www.git-scm.com/book/en/v2/images/commit-and-tree.png)


### 3.1 分支简介

```
git branch testing // 创建 testing 分支

git log --oneline --decorate // 命令查看各个分支当前所指的对象

git checkout testing // 切换分支

git checkout -b testing // 简写，新建分支并切换到该分支上

git log --oneline --decorate --graph --all // 输出你的提交历史、各个分支的指向以及项目的分支分叉情况
```

### 3.2 分支的新建与合并

```
git checkout -b iss53 // 创建并切换到 #53
```






finished the new footer [issue 53]










---

[VIM中的保存和退出、VIM退出命令、如何退出vim编辑、VIM命令大全](https://blog.csdn.net/feosun/article/details/73196299)

> 退出命令是，按ESC键 跳到命令模式，然后输入:q（不保存）或者:wq（保存） 退出。  
> 注意：输入法英文状态下

更多退出命令：
- :w 保存文件但不退出vi 
- :w file 将修改另外保存到file中，不退出vi 
- :w! 强制保存，不推出vi 
- :wq 保存文件并退出vi 
- :wq! 强制保存文件，并退出vi 
- :q 不保存文件，退出vi 
- :q! 不保存文件，强制退出vi 
- :e! 放弃所有修改，从上次保存文件开始再编辑命令历史
