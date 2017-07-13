# Git初始化参数

* --git-dir=Git的仓库路径
* --work-tree=Git的工作路径

上面连个两个参数可以显示的用在初始化,检出,恢复等命令中 . 最简单的例子就是节省git clone的一些不必要的开销 . 使用work-tree , 在仓库状态为git checkout或者git reset指定工作目录即可 .

举个例子 :

```
# 用Laravel库做实验
git clone git@github.com:laravel/laravel.git
# 将仓库的master分支copy到其他目录中
mkdir -p backup
cd laravel
# 查看工作区的状态,会发现少了很多文件,因为没有文件
git --git-dir=.git --work-tree=../backup status
# 检出master分支到工作目录,同时创建tmp分支
git --git-dir=.git --work-tree=../backup checkout -b tmp -f master
# 删除这个分支
git --git-dir=.git --work-tree=../backup branch -d tmp
# 现在就备份了一份完整的master分支.而且没有版本控制

# 还有一种方法就是reset到当前版本,当然reset会对视commit前的内容,reset前还是要注意一下
git --git-dir=.git --work-tree=../backup reset --quiet --hard
```

总之 , 指定你的仓库 , 选择你的Working Tree . 

