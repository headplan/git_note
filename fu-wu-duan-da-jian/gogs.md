# 关于Gogs

Gogs \(Go Git Service\) 是一款极易搭建的自助 Git 服务。

* 使用 Go 语言开发
* 支持全平台

官网:[https://gogs.io/](https://gogs.io/)

Github:[https://github.com/gogits/gogs](https://github.com/gogits/gogs)

## 安装

### 环境要求

#### 数据库

* MySQL
* PostgreSQL
* 直接使用SQLite3或TiDB

> 注:数据库编码应设置为`utf8mb4`

#### Git

* 服务端和客户端版本&gt;=1.7.1

> **MacOS**
>
> brew updata
>
> brew install git
>
> **Debian/Ubuntu**
>
> sudo apt-get update
>
> sudo apt-get install git
>
> Windows:下载安装git-scm.com/downloads

#### SSH服务器

* **如果您只使用 HTTP/HTTPS 或者内置 SSH 服务器的话请忽略此项**
* 推荐Windows系统使用[Cygwin OpenSSH](http://docs.oracle.com/cd/E24628_01/install.121/e22624/preinstall_req_cygwin_ssh.htm)或[Copssh](https://www.itefix.net/copssh)

## 二进制安装

所有的版本都支持**MySQL**和**PostgreSQL**作为数据库,并且均使用构建标签\(build tags\)`cert`进行构建.需要注意的是,不同的版本的支持状态有所不同,请根据实际的Gogs提示进行操作.

#### 下载安装

下载地址:[https://github.com/gogits/gogs/releases/tag/v0.9.113~](https://github.com/gogits/gogs/releases/tag/v0.9.113~)

解压压缩包,进入目录,执行命令

```
./gogs web
```

#### 升级软件

* 下载最新版的压缩包
* 删除当前的`templates`目录
* 解压压缩包并将所有内容复制粘贴到相应\(当前\)的位置



