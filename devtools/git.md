
冲突产生原因：
如果两个人同时更改了同一个文件的同一行代码，或同时添加了一个相同文件名的文件，或者一个人改动了那些被另一个人删除了的代码，Git 就不能简单地确定到底谁的改动才是正确的。这时 Git 会把这些地方标记为一个冲突，你必须首先解决掉这些冲突，然后再继续你的工作。

撤销某次合并：

你应该始终牢记，你可以在任何时间执行撤销操作，并返回到你开始合并之前的状态。要对自己有信心，你不会破坏项目中的任何东西。只要在命令行界面中键入 “git merge --abort” 命令，你的合并操作就会被安全的撤销。
当你解决完冲突，并且在合并完成后发现一个错误，你仍然还是有机会来简单地撤销它。你只须要键入 “git reset --hard ” 命令，系统就会回滚到那个合并开始前的状态，然后重新开始吧！

git merge --abort #如果Git版本 >= 1.7.4
git reset --merge #如果Git版本 >= 1.6.1

git branch -m old new 本地分支重命名，将本地old分支重命名为new

git reset --hard HASH #返回到某个节点，不保留修改。
git reset --soft HASH #返回到某个节点。保留修改

舍弃本地修改：
先git reset —hash
再git checkout .

解决冲突：
例如线上分支test，自己分支sm，sm合并到test有冲突，先使用git fetch origin test:test拉取线上代码到本地的test分支，再使用git checkout test切换到test分支，git branch看一下当前分支为test，
然后git merge sm将本地sm分支合并到test分支，在test分支上修改冲突代码，修改完后再git add .  / git commit -m “解决冲突”.    git push origin test即可。

删除本地分支：
（1）删除一个已被终止的分支
如果需要删除的分支不是当前正在打开的分支，使用branch -d直接删除
git branch -d <branch_name>
（2）删除一个正打开的分支
如果我们在试图删除一个分支时自己还没转移到另外的分支上，Git就会给出一个警告，并拒绝该删除操作。
如果坚持要删除该分支的话，就需要在命令中使用-D选项。
git branch -D <branch_name>



删除远程分支：
git push origin —delete 远程分支名

恢复远程已删分支：
Git会自行负责分支的管理，所以当我们删除一个分支时，Git只是删除了指向相关提交的指针，但该提交对象依然会留在版本库中。
因此，如果我们知道删除分支时的散列值，就可以将某个删除的分支恢复过来。在已知提交的散列值的情况下恢复某个分支：
git branch <branch_name> <hash_val>
如果我们不知道想要恢复的分支的散列值，可以用reflog命令将它找出来

如果使用git reflog也找不到删除分支的（commit id的）哈希值，可以先从线上分支online切出来一个与删除分支同名的分支，去Merge Request找最近一次合到该分支的commit id，然后使用如下命令恢复已被删除的远程分支：
git branch <删除的分支名> <删除分支的哈希值hash_val>

参考：
https://www.cnblogs.com/utank/p/7880441.html