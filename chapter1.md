# 快速应用

Repeat Command中已经有了很详细的整理 , 这里只做补充说明 .

#### **配置Git**

```
# 在 Git 命令中开启颜色显示
git config --global color.ui true
# Git 默认使用emacs作为编辑器,这里改为vim
git config --global core.editor "vim"
# 查看所有配置
git config --list

# 配置中还有--system和--local两个选项
# --system生成配置到/etc/中
# --local是在项目中的.git/config
```

更多关于git config的配置

[http://classfoo.com/ccby/article/2KembSA](http://classfoo.com/ccby/article/2KembSA)

#### 工作流程

```
git init
git add .
git commit -m"a"
git log
git status
```

#### 修正错误的commit

```
# 这里的三个配置也就是三种状态
git reset --hard HEAD^ # 直接回撤到上一个版本
git reset --sort HEAD^ # 回撤到上一个版本commit之前
git reset --mixed HEAD^ # 回撤到上一个版本add之前

# 这里的HEAD在Repeat Command中已有记录,HEAD^表示上一个版本,也可以写为HEAD~1
# HEAD也可以用版本commit的hash值
# 撤回的基本目的是撤回commit,前面只是根据配置参数分开了集中状态,之后要需要重新提交commit
# 如果本次commit中有错误,不希望额外的commit,可以在commit后使用--amend参数,修改本次commit
git commit --amend
# 这里就进入了前面git config配置的vim编辑器了
# vim保存退出后,完成commit
git log
# commit数不变
```

**忽略文件**

这里指的就是.gitignore文件 , 添加到里面的文件就不会被加入到版本控制中 . 还可以在home下创建全局忽略.gitignore\_global

```
*~
.DS_Store
```

避免意外提交泄露信息等 . 

这里用到一个删除命令 , 用来删除已经添加到版本控制中的文件或文件夹 , 对于将其添加到.gitignore之前很有用

```
gir rm --cached [file]
gir rm -r --cached [dir]
```



