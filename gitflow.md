##Git工作流
- Git常用规范
（1）使用 Git 过程中，必须通过创建分支进行开发，坚决禁止在主干分支上直接开发。review 的同事有责任检查其他同事是否遵循分支规范。
（2）在 Git 中，默认是不会提交空目录的，如果想提交某个空目录到版本库中，需要在该目录下新建一个 .gitignore 的空白文件，就可以提交了。
（3）把外部文件纳入到自己的 Git 分支来的时候一定要记得是先比对，确认所有修改都是自己修改的，然后再纳入。不然，容易出现代码回溯。
（4）多人协作时，不要各自在自己的 Git 分支开发，然后发文件合并。正确的方法应该是开一个远程分支，然后一起在远程分支里协作。不然，容易出现代码回溯（即别人的代码被覆盖的情况）。
（5）每个人提交代码是一定要 git diff 看提交的东西是不是都是自己修改的。如果有不是自己修改的内容，很可能就是代码回溯。
（6）review 代码的时候如果看到有被删除掉的代码，一定要确实是否是写代码的同事自己删除的。如果不是，很可能就是代码回溯。

- Git的工作原理

（1）Git的命令工作流程图
![](/assets/GitFlow.PNG)
##### 初始化 
git init // 创建
git clone /path/to/repository // 检出
git config --global user.email "you@example.com" // 配置 email
git config --global user.name "Name" // 配置用户名

##### 操作
git add <file> // 文件添加，A → B
git add . // 所有文件添加，A → B

git commit -m "代码提交信息" // 文件提交，B → C
git commit --amend // 与上次 commit 合并, *B → C

git push origin master // 推送至 master 分支, C → D
git pull // 更新本地仓库至最新改动， D → A
git fetch // 抓取远程仓库更新， D → C

git log // 查看提交记录
git status // 查看修改状态
git diff// 查看详细修改内容
git show// 显示某次提交的内容

##### 撤销操作
git reset <file>// 某个文件索引会回滚到最后一次提交， C → B
git reset// 索引会回滚到最后一次提交， C → B
git reset --hard // 索引会回滚到最后一次提交， C → B → A
 git reset --hard origin/master //放弃本地修改，保持和master版本一致

git checkout // 从 index 复制到 workspace， B → A
git checkout -- files // 文件从 index 复制到 workspace， B → A
git checkout HEAD -- files // 文件从 local repository 复制到 workspace， C → A

##### 分支相关
git checkout -b branch_name // 创建名叫“branch_name” 的分支，并切换过去 
git checkout master // 切换回主分支
git branch -d branch_name // 删除名叫“branch_name” 的分支
git push origin branch_name // 推送分支到远端仓库
git merge branch_name // 合并分支 branch_name 到当前分支(如 master)
git rebase // 衍合，线性化的自动， D → A

##### 冲突处理
git diff // 对比 workspace 与 index
git diff HEAD // 对于 workspace 与最后一次 commit
git diff <source_branch> <target_branch> // 对比差异
git add <filename> // 修改完冲突，需要 add 以标记合并成功

##### 其他
gitk // 开灯图形化 git
git config color.ui true // 彩色的 git 输出
git config format.pretty oneline // 显示历史记录时，每个提交的信息只显示一行
git add -i // 交互式添加文件到暂存区

## Git的团队合作