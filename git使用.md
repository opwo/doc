# 生成ssh

```sh
ssh-keygen -t rsa -C "youremail@example.com" #邮箱是注册GitHub的邮箱
```

生成后会在C盘当前用户目录下生成`.ssh`文件夹。复制`id_rsa.pub`里面的内容到github里边。

![](./img/ssh1.png)

![](./img/githubssh.png)