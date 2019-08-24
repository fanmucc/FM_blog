## Git 命令
详细教程请看[Git命令](https://www.yiibai.com/git/git_push.html)
#### 克隆一个项目
```git
git clone + 项目地址
```

#### 查看分支
```git
// 查看本地分支
git branch
// 查看远程分支
git branch -r
// 列出本地分支和远程所有分支
git branch -a
```

#### 分支操作
```git
// 创建本地分支
git branch [分支名]    // 创建分支，但不会切换到创建的分支上；
git branch -b [分支名] // 创建分支，但会跳转到所创分支上；

// 创建远程分支
git push origin [分支名] // 创建远程分支，但不会切换到创建的分支上(线上代码库由专业人员进行处理，勿操作);

// 切换分支
git checkout [分支名]  // 切换分支
git checkout -        // 切换上一个分支

// 切换远程分支
git checkout -b [本地分支] [远程分支名]     // 新建本地分支(切换至新建分支上) 切换远程分支
// 删除分支
git branch -d [分支名] // 删除分支
git branch -D [分支名] // 强制删除

// 删除远程分支
git push origin --delete [分支名]  // 删除远程分支(勿操作)
git branch -dr origin/[分支名]     // 删除远程分支(勿操作)
```

## 分支提交与合并
### 提交
```git
// 提交
git add .                         // 添加当前目录的所有文件到暂存区
git add [文件名] [文件名]...        // 添加指定文件到暂存区


git commit -m [备注]               // 提交暂存区到仓库区
git commit [文件名] [文件名] ... -m [备注]  // 提交暂存区的指定文件到仓库区

git push <远程主机名> <本地分支名>:<远程分支名>  // 将本地代码提交到远程仓库

// 如果省略本地分支名 则起到删除远程分支的作用
例: git push origin :dev;   //则删除远程dev分支  
等同于
git push origin --delete dev;
```
### 合并
```git
// 本地代码合并
// dev 合并到 master
// 先切换到master分支下
git checkout master;        // 切换分支
git merge dev;              // 合并分支
```

## 提交冲突
!> 提交代码要慎重，此问题主要发生在，本地代码和远程分支代码有文件不同所造成的，即提交之前为拉去最新的远程代码
### 更新本地代码
```git
// 拉去代码
git pull <远程主机名> <本地分支名>:<远程分支名>;    // 慎重，每次提交之前都要拉去一下远程仓库代码
```
### 解决冲突
// 不全面，往后会进一步更新；
```git
git status                  // 能够查看本地那些文件被修改
// 同时如果有冲突的话会进行提示
On branch dev
Your branch and 'origin/dev' have diverged,
and have 1 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)          //中止合并

Unmerged paths:
  (use "git add <file>..." to mark resolution)          // 未合并的通过 git add [文件名]... 进行分辨

	both modified:   README.md                  // 指出远程和本地都进行修改过的文件，基本就是冲突文件

// 执行
// 方案1
git merge --abort           // 中止合并, 此命令会将本地代码恢复，所以执行前进行进行复制
下面执行正常的更新代码和提交；


git diff                    // 会查找到冲突的具体细节，将其删除掉

// 方案2
合同协作的两人，前后都对一段代码进行了维护或添加，第二个人就会在此提交就会提示
让其拉取最新代码，但两人文件势必会发生冲突，所以我们借助第三方，建立一个新的分
支将线上代码同步进去，然后和本地写文件的代码进行合并，协同两人排除相应的代码排
除冲突；

git branch -b [第三方分支名]
git pull origin [远程分支名]:[远程分支名]
git checkout [本人代码写作分支]
git merge [第三方分支名]
git diff        // 进行修改；
```

