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
git push origin testing // 将本地 testing 分支推送到远程 origin
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

git commit -a -m 'added a new footer [issue 53]' // 创建一个新分支指针

git checkout master // 切换到mester，创建分支修复一个紧急bug
git checkout -b hotfix
git commit -a -m 'fixed the broken email address'
git checkout master
git merge hotfix // 从 hotfix 分支合并代码
git branch -d hotfix // 删除分支

git checkout iss53 // 切换回 iss53 继续开发
git commit -a -m 'finished the new footer [issue 53]'

git checkout master // 切换到master，将 iss53 分支合并到 master
git merge iss53
git branch -d iss53
```

##### 遇到冲突时的分支合并

有时候合并操作不会如此顺利。 如果你在两个不同的分支中，对同一个文件的同一个部分进行了不同的修改，Git 就没法干净的合并它们。 如果你对 #53 问题的修改和有关 hotfix 的修改都涉及到同一个文件的同一处，在合并它们的时候就会产生合并冲突
```
git merge iss53

git status // 查看那些因包含合并冲突而处于未合并（unmerged）状态的文件

$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)

    both modified:      index.html

no changes added to commit (use "git add" and/or "git commit -a")
```

```
// 特殊区段
<<<<<<< HEAD:index.html
<div id="footer">contact : email.support@github.com</div>
=======
<div id="footer">
 please contact us at support@github.com
</div>
>>>>>>> iss53:index.html
```
这表示 HEAD 所指示的版本（也就是你的 master 分支所在的位置，因为你在运行 merge 命令的时候已经检出到了这个分支）在这个区段的上半部分（======= 的上半部分），而 iss53 分支所指示的版本在 ======= 的下半部分。 为了解决冲突，你必须选择使用由 ======= 分割的两部分中的一个，或者你也可以自行合并这些内容。 例如，你可以通过把这段内容换成下面的样子来解决冲突：
```
<div id="footer">
please contact us at email.support@github.com
</div>
```
上述的冲突解决方案仅保留了其中一个分支的修改，并且 <<<<<<< , ======= , 和 >>>>>>> 这些行被完全删除了。 在你解决了所有文件里的冲突之后，对每个文件使用 git add 命令来将其标记为冲突已解决。 一旦暂存这些原本有冲突的文件，Git 就会将它们标记为冲突已解决。

如果你想使用图形化工具来解决冲突，你可以运行 git mergetool，该命令会为你启动一个合适的可视化合并工具，并带领你一步一步解决这些冲突：

```
$ git mergetool

This message is displayed because 'merge.tool' is not configured.
See 'git mergetool --tool-help' or 'git help config' for more details.
'git mergetool' will now attempt to use one of the following tools:
opendiff kdiff3 tkdiff xxdiff meld tortoisemerge gvimdiff diffuse diffmerge ecmerge p4merge araxis bc3 codecompare vimdiff emerge
Merging:
index.html

Normal merge conflict for 'index.html':
  {local}: modified file
  {remote}: modified file
Hit return to start merge resolution tool (opendiff):
```
如果你想使用除默认工具（在这里 Git 使用 opendiff 做为默认的合并工具，因为作者在 Mac 上运行该程序）外的其他合并工具，你可以在 “下列工具中（one of the following tools）” 这句后面看到所有支持的合并工具。 然后输入你喜欢的工具名字就可以了。
等你退出合并工具之后，Git 会询问刚才的合并是否成功。 如果你回答是，Git 会暂存那些文件以表明冲突已解决： 你可以再次运行 git status 来确认所有的合并冲突都已被解决：

```
$ git status
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:

    modified:   index.html
```
如果你对结果感到满意，并且确定之前有冲突的的文件都已经暂存了，这时你可以输入 git commit 来完成合并提交。 默认情况下提交信息看起来像下面这个样子：

```
Merge branch 'iss53'

Conflicts:
    index.html
#
# It looks like you may be committing a merge.
# If this is not correct, please remove the file
#	.git/MERGE_HEAD
# and try again.


# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# All conflicts fixed but you are still merging.
#
# Changes to be committed:
#	modified:   index.html
#
```

### 3.3 分支管理

```
git branch // 获取所有分支的一个列表，* 表示现在检出的一个分支（即，当前 HEAD 指针所指向的分支）
git branch -v // 查看每一个分支的最后一次提交

git branch --merged // --merged 和 --no-merged 过滤这个列表中已经合并或尚未合并到当前分支的分支
```

### 3.4 分支开发工作流

##### 长期分支
![image](https://www.git-scm.com/book/en/v2/images/lr-branches-2.png)
渐进稳定分支的流水线（“silo”）视图

##### 特性分支（短期分支）
![image](https://www.git-scm.com/book/en/v2/images/topic-branches-1.png)

### 3.5 远程分支

```
git fetch origin // 查找 “origin” 是哪一个服务器，从中抓取本地没有的数据，并且更新本地数据库，移动 origin/master 指针指向新的、更新后的位置。

git pull // 从远程拉取并合并到当前分支，git pull可以看成git fetch和git merge两个步骤的结合

git checkout -b testing // 新建并切换分支
git checkout -b testing origin/testing // 以远程跟踪分支为基础，新建并切换分支（起点位于 origin/testing）

git checkout --track origin/testing // git checkout -b testing origin/testing 的快捷方式

git branch -u origin/testing // -u 或 --set-upstream-to 切换当前分支跟踪的远程分支（从跟踪 master 更改为跟踪 testing）

git branch -vv // 查看所有分支跟踪的远程分支，且包含更多的信息，如每一个分支正在跟踪哪个远程分支与本地分支是否是领先、落后或是都有

git push origin --delete testing // 运行带有 --delete 选项的 git push 命令来删除一个远程分支
```

### 3.6 变基

在 Git 中整合来自不同分支的修改主要有两种方法：merge 以及 rebase。

![image](https://www.git-scm.com/book/en/v2/images/basic-rebase-1.png)

以上 主干master分支 和 临时experiment 分支，需要将 experiment 整合到主干。

1. merge 命令：  
    它会把两个分支的最新快照（C3 和 C4）以及二者最近的共同祖先（C2）进行三方合并，合并的结果是生成一个新的快照（C5）（并提交）
![image](https://www.git-scm.com/book/en/v2/images/basic-rebase-2.png)
2. rebase 命令：  
    你可以提取在 C4 中引入的补丁和修改，然后在 C3 的基础上应用一次。将提交到某一分支上的所有修改都移至另一分支上，就好像“重新播放”一样。
![image](https://www.git-scm.com/book/en/v2/images/basic-rebase-3.png)

```
git branch experiment // 新建 临时experiment

git commit -a -m "C3" // master 提交记录 C3

git checkout experiment // 切换到 experiment 分支

git commit -a -m "C4" // master 提交记录 C4

git rebase master // 将 experiment 分支变基到 目标基底分支 master

git status // 确认所有的合并冲突都已被解决

git mergetool // 打开合并工具解决冲突，输入 Beyond Compare，打开指定的合并工具

git add * // 将所有文件添加到暂存区

git rebase --continue // 继续变基（衍和）

git checkout master // 切换到 master

git merge experiment // 进行一次快进合并
```

git rebase master 它的原理是首先找到这两个分支（即当前分支 experiment、变基操作的目标基底分支 master）的最近共同祖先 C2，然后对比当前分支相对于该祖先的历次提交，提取相应的修改并存为临时文件，然后将当前分支指向目标基底 C3, 最后以此将之前另存为临时文件的修改依序应用。（译注：写明了 commit id，以便理解）

![image](https://www.git-scm.com/book/en/v2/images/basic-rebase-4.png)

1. 它们看上去就像是串行的一样，提交历史是一条直线没有分叉
2. 目的是为了确保在向远程分支推送时能保持提交历史的整洁


![image](https://www.git-scm.com/book/en/v2/images/interesting-rebase-1.png)

```
git rebase --onto master server client // git rebase --onto [basebranch] [otherbranch] [topicbranch] 选中在 client 分支里但不在 server 分支里的修改（即 C8 和 C9），将它们在 master 分支上重放

git checkout master

git merge client
```

以上命令的意思是：“取出 client 分支，找出处于 client 分支和 server 分支的共同祖先之后的修改，然后把它们在 master 分支上重放一遍”。

![image](https://www.git-scm.com/book/en/v2/images/interesting-rebase-2.png)

```
git rebase master server // git rebase [basebranch] [topicbranch] 将特性分支（即本例中的 server）变基到目标分支（即 master）上
```

![image](https://www.git-scm.com/book/en/v2/images/interesting-rebase-4.png)

```
git checkout master
git merge server

git branch -d client // 删除分支
git branch -d server // 删除分支
```

![image](https://www.git-scm.com/book/en/v2/images/interesting-rebase-5.png)


==**不要对在你的仓库外有副本的分支执行变基**==







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
