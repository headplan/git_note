# 部署记录

参考资料

[https://mynook.info/blog/post/host-your-own-git-server-using-gogs](https://mynook.info/blog/post/host-your-own-git-server-using-gogs)

安装过程分为这些步骤:

* 新建用户;
* 下载源码编译 / 下载预编译二进制打包;
* 运行安装;
* 配置调整;
* 配置nginx反向代理;
* 保持服务运行;

##### 新建用户

```
sudo adduser git
su git
mkdir .ssh
```

##### 下载二进制包

```
wget http://7d9nal.com2.z0.glb.qiniucdn.com/gogs_v0.9.113_linux_amd64.zip
unzip gogs_v0.9.113_linux_amd64.zip
ls /home/git/gogs
```

##### 运行安装

```
cd /home/git/gogs
mysql -u root -p < scripts/mysql.sql
# 登录数据库,创建gogs用户赋予root权限,这里的localhost是用户允许访问的地址
create user 'gogs'@'127.0.0.1' identified by '密码';
grant all privileges on gogs.* to 'gogs'@'127.0.0.1';
flush privileges;
# 退出数据库
./gogs web
# 然后访问ip:3000开始安装
# 这里给防火墙加了3000端口
    # 允许8080端口
    iptables -I INPUT 4 -p tcp -m state --state NEW -m tcp --dport 8080  -j ACCEPT
    # 保存iptables规则
    service iptables save
    # 查看iptables规则
    iptables -nvL

# 安装时数据库权限出了点问题,修改了mysql.user中的host字段解决了问题.现在一切正常.
```

##### 调整配置

配置文件位于Gogs目录的`custom/conf/app.ini`

常用配置

* `RUN_USER`默认是`git`,指定Gogs以哪个用户运行
* `ROOT`所有仓库的存储根路径
* `PROTOCOL`如果你使用 nginx 反代的话请使用`http`,如果直接裸跑对外服务的话随意
* `DOMAIN`域名.会影响SSH clone地址
* `ROOT_URL`完整的根路径,会影响访问时页面上链接的指向,以及HTTP clone的地址
* `HTTP_ADDR`监听地址,使用nginx的话建议`127.0.0.1`,否则`0.0.0.0`也可以
* `HTTP_PORT`监听端口,默认`3000`
* `INSTALL_LOCK`锁定安装页面
* Mailer 相关的选项

详细的配置:[https://gogs.io/docs/advanced/configuration\\_cheat\\_sheet.html](https://gogs.io/docs/advanced/configuration_cheat_sheet.html)

##### Nginx反向代理

```
server {
    server_name 域名或IP;
    listen 80; # 或者 443，如果你使用 HTTPS 的话
    # ssl on; 是否启用加密连接
    # 如果你使用 HTTPS，还需要填写 ssl_certificate 和 ssl_certificate_key

    location / { # 如果你希望通过子路径访问，此处修改为子路径，注意以 / 开头并以 / 结束
        proxy_pass http://127.0.0.1:3000/;
    }
}
```

然后重启nginx

##### 脚本服务

将`./gogs/scripts/init`的脚本复制到`/etc/init.d`下,给予执行权限并修改相关参数,启动服务:

```
sudo service gogs start
```

**hosts绑定**

如果是反向代理内部访问 , 还需要绑定本地hosts .

