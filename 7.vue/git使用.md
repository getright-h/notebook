## git

### 1.创建版本库

1. `git init` 初始化仓库
2. `git add xxx(file)` 把文件添加到仓库(暂存区)
3. `git commit -m"描述信息" ` 把文件提交到仓库(当前分支)



### 2.时光穿梭

`git status` 查看当前的状态

`git diff` 查看修改的地方有哪些

当检查无误之后再提交

#### 2.1版本退回

1. `git log` 查看版本
2. `git reset --hard HEAD^` 回到指定版本号
   1. HEAD^ 在windows中会失效，换成~即可
   2. ~表示上一个，~x表示上x个版本
   3. 这里的head也可以替换成具体的版本号
3. `git reflog` 查看版本历史操作(用于重启后查看想退回的版本)



#### 2.2工作区 暂存区

add命令是把文件添加到了暂存区，commit是把文件添加到了当前分支上

使用了add之后，仓库的状态如下：

![git-stage](assets/0.jpg)

使用了commit，仓库状态如下：

![git-stage-after-commit](assets/0-1652428357187.jpg)

#### 2.3管理修改

git跟踪管理的是修改，而非文件

当每次add了之后，请立即commit，如果add了之后，在进行修改，这次修改的东西就不会被提交到当前分支



#### 2.4 删除修改

1. 只是在工作区修改了(本地，且没add)

   手动删除后，`git checkout --filename` checkout其实使用版本库里的最新版本替代当前

2. 提交了暂存区(add之后)

   `git reset HEAD filename` 此时暂存区还原了，工作区还有修改

   重复第一步，清除工作区的修改



#### 2.5删除文件

1. 你删错了，想要还原

   `git checkout -- filename` checkout是从版本库中获取最新版本用于替代当前

2. 你就是想删除

   `git rm filename` 删除版本库中的文件

   `git commit` 并且提交



### 3.远程仓库

#### 3.1推送到远程

在github上创建一个远程仓库，

1. 在本地目录下执行

   ```
   git remote add origin git@github.com:getright-h/learngit.git
   ```

2. 把本地推送到远程

   第一次用`-u`

   `git push -u origin master`



#### 3.2clone

从远程克隆一个仓库

`git clone 仓库地址`



### 4.分支管理

#### 4.0创建合并

- `git branch` 查看分支
- `git switch -c xxx` 创建并切换到xxx分支
- `git switch master` 回到主分支
- `git merge xxx` 把xxx分支合并到当前分支下
- `git brancg -d xxx` 删除xxx分支
- `git pull origin 远程分支:本地分支` 同名简写 `git pull origin 本地分支`

#### 4.1git fetch和git pull的区别

**git fetch**

git fetch：相当于是从远程获取最新版本到本地，不会自动合并。

```
$ git fetch origin master
$ git log -p master..origin/master
$ git merge origin/master
123
```

以上命令的含义：

首先从远程的origin的master主分支下载最新的版本到origin/master分支上然后比较本地的master分支和origin/master分支的差别最后进行合并
上述过程其实可以用以下更清晰的方式来进行：

```
$ git fetch origin master:tmp
$ git diff tmp 
$ git merge tmp
123
```

**git pull**
git pull：相当于是从远程获取最新版本并merge到本地
git pull origin master
Shell
上述命令其实相当于git fetch 和 git merge在实际使用中，git fetch更安全一些，因为在merge前，我们可以查看更新情况，然后再决定是否合并。



#### 4.2解决冲突

当主分支和其他分支产生冲突时，需要我们手动更改来解决

![git-br-feature1](assets/0.png)

此时两者都有了新的提交，git无法快速合并，必须手动解决，解决后如下：

![git-br-conflict-merged](assets/0-1652434932908.png)



#### 4.3分支策略

在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本；

你和你的小伙伴们每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

所以，团队合作的分支看起来就像这样：

![git-br-policy](assets/0-1652435688865.png)



#### 4.4bug分支

开发中，有时需要我们停下手中的工作，来拉一个新分支修复某个bug，但是这时我们的dev又不能提交。这时需要用把工作区暂存起来

1. `git stash` 把工作区暂存起来
2. 在master上拉取解决bug的分支 issue-xxx
3. 解决后把这个issue-xxx分支合并给master
   1. 因为dev是master上拉去的，这里我们可以顺便把dev上存在的同样的bug修复了
   2. `git cherry-pick <修复bug时的提交id>` 切换到dev，这里复制之前在issue上修复bug的提交id，这样可以重复修复bug的操作给dev分支
      1. `git stash list` 可以查看有几个暂存区
   3. `git stash pop` 回复当前暂存的工作区的同时，删除此暂存工作区





#### 4.5多人协作

https://www.liaoxuefeng.com/wiki/896043488029600/900375748016320

工作模式通常是这样：

1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！

如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。



### 5.标签管理

待后续完善





### 6. 一些小问题

#### 6.1 ignore不生效

.gitignore中已经标明忽略的文件目录下的文件，git push的时候还会出现在push的目录中，或者用git status查看状态，想要忽略的文件还是显示被追踪状态。
原因是因为在git忽略目录中，新建的文件在git中会有缓存，如果某些文件已经被纳入了版本管理中，就算是在.gitignore中已经声明了忽略路径也是不起作用的，
这时候我们就应该先把本地缓存删除，然后再进行git的提交，这样就不会出现忽略的文件了。



**解决方法: git清除本地缓存（改变成未track状态），然后再提交:**

```js
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
git push -u origin master
```

需要特别注意的是：
1）.gitignore只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。
2）想要.gitignore起作用，必须要在这些文件不在暂存区中才可以，.gitignore文件只是忽略没有被staged(cached)文件，
对于已经被staged文件，加入ignore文件时一定要先从staged移除，才可以忽略。