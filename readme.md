1. 创建仓库
git init
2. 添加文件到仓库
git add readme.md
可以多次添加，一次可以添加多个文件
3. 提交文件到仓库
git commit -m 'add readme.md'
4. 查看仓库目前状态
git status
5. 查看修改内容
git diff readme.md
6. 查看提交记录
git log
7. 版本回退
* HEAD：当前版本
* HEAD^：上个版本
* HEAD^^：上上个版本
* HEAD~100：上100个版本
* git reset --hard HEAD^ 回退到上个版本
* git reflog 查看命令历史，找到每次commit的ID，可以指定reset到某个版本
* git reset --hard commit_id
8. 工作区与暂存区
* 工作区：本地git项目目录
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
