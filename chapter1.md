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

# 删除配置可以使用
git config --global --unset alias.un
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

#### **忽略文件**

这里指的就是.gitignore文件 , 添加到里面的文件就不会被加入到版本控制中 . 还可以在home下创建全局忽略.gitignore\_global

```
*~
.DS_Store
# 还要添加到配置中
[core]
    excludesfile=/Users/headplan/.gitignore_global
```

避免意外提交泄露信息等 .

这里用到一个删除命令 , 用来删除已经添加到版本控制中的文件或文件夹 , 对于将其添加到.gitignore之前很有用

```
gir rm --cached [file]
gir rm -r --cached [dir]
```

之后可以添加到ignore文件,或者物理删除文件,再commit即可.

#### 分支管理

Repeat Command中对Git的分支以及分支策略的描述已经很到位 .

#### 解决冲突

Repeat Command中对Git的解决冲突的流程描述已经很到位 .

#### 储藏功能

Repeat Command中对Git stash的流程描述已经很到位 .

#### git rebase

和git merge一样都可以合并分支 , merge的意思是合并两个分支 , 即合并主分支和dev分支 , log会有记录merge . 而rebase是将分支合并到当前分支 , 就像在当前分支commit一样 , log里也不会记录有merge的痕迹 , 即让分支历史看起来像没有经过任何合并一样 . 

```
git rebase dev
# 当然和merge一样,rebase也会产生冲突,解决方法是
# (master) git rebase --skip # 意思是以dev的commit解决冲突
# (master) git rebase --abort # 意思是保持不变,保留master的commit.

# (master) git rebase --continue # 字面意思是跳过的意思
# 这里产生跳过的方式是在git rebase dev发生冲突之后,修改缓存中的源码和dev相同,就会出现跳过的方式.
# 会在.git中生成文件.git/rebase-apply
# 之后再在master使用git rebase dev.会直接跳过
# 如果修改冲突为master或者其他,则会生成两个commit,后一个为dev的commit,之后为HEAD的master的commit

# rebase发生冲突后的流程
(master) git rebase dev
# (ba99d1f) 直接--skip或--abort
(ba99d1f) 修改冲突
(ba99d1f) git add . 
(ba99d1f) git rebase --continue (会直接commit)
```

#### 其他

```
[git log]
# 一行显示,时间轴
git log --oneline
git log --oneline --grahp
# 也可以配置alias显示更友好的log
# 还可以安装tig,显示更友好的log

[Git GUI]
Github
Sourcetree
```



