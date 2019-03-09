
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

