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
git --git-dir=./.git --work-tree=../backup status
```



