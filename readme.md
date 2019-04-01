Github操作
```
1.基本操作
本地端
git init
git add .file
git commit -m "add new files"

远程端
git remote add origin git@github.com:crankler/bolg-ubuntu.git
git push -u origin master


2.查看信息
运行git status命令看看结果
git diff顾名思义就是查看difference
git diff HEAD -- readme.txt命令可以查看工作区和版本库里面最新版本的区别

穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id
上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100
 git reset --hard HEAD^

3.删除或丢弃
 git checkout -- file可以丢弃工作区的修改
 总之，就是让这个文件回到最近一次git commit或git add时的状态。
场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。
场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库

命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。
确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit
错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：git checkout 

先在本地把两个文件删除，然后执行以下命令：
$ git add * //把本地仓库的文件上传到缓存。
$ git commit -m 'del' //把第一步上传到缓存的东西上传到本地仓库，其中'del'是操作标识，内容随便填，方便用户观看。
$ git push origin master //把本地仓库的文件上传到远程仓库

4.分支
Git鼓励大量使用分支：
查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>
创建+切换分支：git checkout -b <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name>
获取远地仓库 git fetch origin/branch name


git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
$ git branch dev
$ git checkout dev

当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
用git log --graph命令可以看到分支合并图。

通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息
加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并

开发一个新feature，最好新建一个分支；
如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。

5.多人合作
首先，可以试图用git push origin <branch-name>推送自己的修改；
如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
如果合并有冲突，则解决冲突，并在本地提交；
没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，
用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。


查看远程库信息，使用git remote -v；
在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。


6.标签
命令git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id；
命令git tag -a <tagname> -m "blablabla..."可以指定标签信息；
命令git tag可以查看所有标签。
用git show <tagname>查看标签信息

命令git push origin <tagname>可以推送一个本地标签；
命令git push origin --tags可以推送全部未推送过的本地标签；
命令git tag -d <tagname>可以删除一个本地标签；
命令git push origin :refs/tags/<tagname>可以删除一个远程标签。

```

参考
[廖雪峰 git](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000).