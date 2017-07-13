# Git Submodule

> **参考资料**
>
> [http://www.kafeitu.me/git/2012/03/27/git-submodule.html](http://www.kafeitu.me/git/2012/03/27/git-submodule.html)

使用Git Submodule功能实现多个子系统\(模块\)都能及时更新到最新的公共资源 .

### Git Submodule功能测试流程记录

```
# 准备环境
mkdir -p submd/repos
# 创建本地仓库,选项--bare的意思是创建裸库
# 裸库只保存git历史提交的版本信息,多用在远端仓库中
# 在裸库中进行git操作会报错然你去工作区执行
git --git-dir=lib1.git init --bare
git --git-dir=lib2.git init --bare
git --git-dir=project1.git init --bare
git --git-dir=project2.git init --bare

# 初始化项目工作区
mkdir -p submd/working
cd working
# 克隆项目1,会提示是个空的库.添加些内容
git clone ../repos/project1.git
cd project1
echo "project1" > project-infos.txt
git add project-infos.txt
git st
git commit -m"init project1"
# 最后提交到仓库中
git push origin master
# 克隆项目2,并提交1次
git clone ../repos/project2.git
cd project2
echoggit st
git commit -m"init project2"
# 最后提交到仓库中
git push origin master

# 初始化公共类库,和前面的操作一样
git clone ../repos/lib1.git
cd lib1
echo "I'm lib1." > lib1-features.php
git add lib1-features.php
git commit -m"init lib1"
git push origin master

git clone ../repos/lib1.git
cd lib2
echo "I'm lib2." > lib2-features.php
git add lib2-features.php
git commit -m"init lib2"
git push origin master
```

```
# 为主项目添加Submodules
# 为project1添加lib1和lib2
cd project1
git submodule add ../../repos/lib1.git libs/lib1
git submodule add ../../repos/lib2.git libs/lib2
# 公共库的内容都添加到了项目1
tree libs
# 查看新增的文件
git st
# 这里多了一个.gitmodules文件,用来记录添加的Submodule的路径和仓库地址
# 现在把他们提交到project1的仓库中去
git commit -a -m "add submodules[lib1,lib2] to project1"
git push

# 现在,我们再克隆一份project1仓库的内容到project1-b目录工作,模拟其他人的clone
git clone ../repos/project1.git project1-b
# 发现我们克隆下来的目录结构是完整的,但是libs中的每个lib的文件没有克隆下来
# 查看一下
git submodule
# 看到submodules的状态是hash码和文件目录
# 最前面的减号表示状态为还没检出
# 检出submodule
git submodule init
git submodule update

```



