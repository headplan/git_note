# Git Submodule

> **参考资料**
>
> [http://www.kafeitu.me/git/2012/03/27/git-submodule.html](http://www.kafeitu.me/git/2012/03/27/git-submodule.html)

使用Git Submodule功能实现多个子系统\(模块\)都能及时更新到最新的公共资源 . 

### Git Submodule功能测试流程记录

```
# 准备环境
mkdir -p submd/repos
# 创建本地仓库
git --git-dir=lib1.git init --bare
git --git-dir=lib2.git init --bare
git --git-dir=project1.git init --bare
git --git-dir=project2.git init --bare
```



