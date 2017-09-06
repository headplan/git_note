# 常见问题

#### 解决mac电脑上出现Permission to xxx.git denied to xxx的问题

排除了用户名配置和密钥等问题 , Mac上主要的还是缓存问题 . 解决方案 : 

```
https://help.github.com/articles/updating-credentials-from-the-osx-keychain/
```

输入下面的命令即可 : 

```
$ git credential-osxkeychain erase
host=github.com
protocol=https
[Press Return]
```



