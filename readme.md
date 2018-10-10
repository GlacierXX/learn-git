#### 安装
> mac

homebrew
```shell
brew install git
```

Xcode集成Git
设置->download->Command Line Tools install
> [windows](https://git-scm.com/downloads)

> 命令
1. 创建仓库
git init
2. 添加文件到仓库
git add xxx xxx 添加一个或者多个文件
git add . 添加所有修改和新增(1.x版本不会包括删除文件，2.x版本会包括)
git add -u/--update 更新已经被add过的文件，tracked file
git add -A/--all .和update的组合
3. 提交文件到仓库
git commit -m 'add readme.md'
4. 查看仓库目前状态
git status
5. 查看修改内容
git diff readme.md
6. 查看提交记录
git log
7. 版本回退
> HEAD：当前分支最近的一次提交
> Index： staging area，暂存区，即将要被commit的文件集合
> Working copy：正在工作的文件集，本地文件

reset三个等级：
reset --soft：恢复HEAD指针，Index与Working copy不变
reset --mixed(default)：恢复HEAD指针，Index丢失，Working copy不变
reset --hard：恢复HEAD指针，Index与Working copy修改全部丢失

* HEAD：当前版本
* git reset HEAD^ 回退到上个版本
* HEAD^：上个版本
* HEAD^^：上上个版本
* HEAD~100：上100个版本
* git reflog 查看命令历史，找到每次commit的ID，可以指定reset到某个版本
* git reset commit_id
8. 工作区与暂存区
* 工作区：本地git项目目录， Working copy
* 暂存区：工作区中的.git隐藏目录版本库，其中包括stage称作暂存区，还有git自动创建的第一个分支master，以及指向master的指针HEAD
* git add将工作区中的修改放在暂存区
* git commit将暂存区中的修改提交到分支
* git跟踪并管理的是修改，并不是文件，所以没有使用git add将修改保存在暂存区中的修改，不会被git commit提交到分支
9. 撤销更改
* git checkout -- readme.md
* 修改未添加到暂存区，恢复到上次commit之后
* 修改已经被添加到缓存区，恢复到上次add之后
* git reset HEAD readme.md
* 将添加到暂存区未commit的修改撤销
10. 删除文件
* git rm test.txt
* 误删的文件可以使用reset或者checkout恢复，但是会丢失最后一次更改
11. 创建SSH Key
* ssh-keygen -t rsa -C "youremail@example.com"
* id_rsa 私钥
* id_rsa.pub 公钥
12. 关联远程仓库
* git remote add origin https://github.com/GlacierXX/learn-git.git
* origin是远程库的名字，也可以起别的名字
* 将本地库中master分支推送到远程库中
* git push -u origin master
* -u 参数第一次推送的时候使用，将本地的master分支和远程仓库中的master分支关联起来，之后可以直接git push origin master推送
13. 克隆远程仓库到本地
git clone https://github.com/GlacierXX/learn-git.git
14. 创建切换分支
* 创建并切换到dev分支 git checkout -b dev
* 相当于：
* git branch dev
* git checkout dev
* 查看当前分支 git branch，当前分支前会标有*号
* 合并dev分支到master，首先切换分支到master，然后git merge dev
* 合并后可以删除dev分支，git branch -d dev
15. 解决冲突
* git merge 合并分支时，如无法自动合并，需要解决冲突之后，进行提交
* git log --graph 可以查看分支合并图
16. 分支策略
master：稳定分支，用来发布新版本，不用来开发
dev：不稳定分支，用来开发，将自己的修改合并到dev分支
17. BUG分支
* git stash 存储当前dev分支工作现场
* master上创建临时修复分支，修复后合并，并删除临时分支
* git stash list 查看保存列表
* git stash apply [stash@{0}] 恢复保存内容
* 需要用git stash drop来删除记录
* git stash pop恢复的同时也会删除记录
18. feature分支
* 新功能的开发需要新建feature分支
* 分支合并之前需要删除 git branch -D feature -D表示强制删除
19. 多人协作
* git remote -v 查看远程库信息，不是所有分支都需要推送到远程仓库
* master：主分支需要与远程同步
* dev：开发分支，团队成员都需要基于此分支开发，应该同步
* bug：bug分支只用于本地修复，无需推送，除非需要
* feature：是否推送取决于是否和其他人合作完成
* 1. git push origin dev 推送自己的修改
  2. 远程分支比本地新则需要拉取更新并合并，git pull
  3. 如果合并有冲突则解决冲突后提交
  4. git pull失败，则本地分支和远程分支需要建立关系，git branch --set-upstream-top branchName origin/branchName
20. git rebase 将本地未push的分叉整理成一条直线，使查看历史变的简洁
21. 标签管理
* git tag name commit_id 可以为某次commit打标签，如不指定commit_id，则为HEAD
* git tag -a name -m desc commit_id -m参数可以指定此次tag的描述文字
* git tag 查看标签
* git show name 查看某个tag的详情
* tag只与commit有关，如多个分支都有此次提交则都会被打上tag
* git tag -d name 删除标签
* git push origin name 推送tag到远程
* git push origin --tags 一次性推送全部尚未推送到远程的标签
* 删除远程tag，先要从本地删除，然后git push origin :refs/tags/name
