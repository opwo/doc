# 目的
记录一些信息管理系统项目相关技术博客或者心得。当做线上笔记使用。

# 项目是涉及技术领域
* 前端
* 后端
* 数据处理分析
* 数据库

# 成员及分工
opwo 后端 657835775@qq.com
Doraengineer 数据处理分析 orange_working@163.com
HZJack 数据库 747386797@qq.com
wangying 前端 930126069@qq.com
----------
#项目维护指南
## github简述
[git笔记](https://blog.csdn.net/weixin_42641395/article/details/82429899)
## github使用
### 准备工作
1 fork仓库（fork的仓库只在本地，不会随原仓库更新而更新）
2 github建立ssh(使用ssh clone无需账号密码登陆，将计算机序列号存入github账号中，如果没建立ssh，则使用ssh clone项目时会报错，只能使用HTTP clone 项目，需要重新输入账号密码)
* 进入git，

* 输入  

```

git config --global user.name "yourusername"// 自己写名字

git config --global user.email "youremail@xx.xxx"//github注册邮箱

```

* 生成ssh

```

ssh-keygen -t rsa -C "youremail@xx.xxx"//github注册邮箱

```

* 获取生成key

```

cat ~/.ssh/id_rsa.pub

```

* 复制key

* github 添加SSH
github :头像旁边settings->SSH and GPG keys 将key全部复制进去

上传时候会提示输入登录名密码，其次输入用户名密码


### 配置.git文件 
#### 网上已有项目，第一次下载项目
1 右键，git bash
2 进入新建文件夹创建库

```
git init
```

3 配置git用户名（告诉是谁在用这个库）
```
git config --global user.email "XXX"//github注册邮箱
git config --global user.name "XXX"// 自己写名字
```

4 到github查找项目地址（SSH对应的git地址需要登陆后查看）
5 下载.git到目标文件夹
```
git clone https://github.com/opencv/opencv.git
```
或者
```
git pull https://github.com/opencv/opencv.git
```
#### 网上新建项目，将自己已写好的文件上传到新建项目（新建项目没有内容）
1-3步不变
4 github中新建项目并查看git地址
5 git文件中添加分支
```
git remote add origin git@code.aliyun.com:orange4code/stitching.git
```
###文件修改上传
1.进入下载下来的仓库文件夹进行修改，添加到缓存区（缓存区，可以多次add，最后在commit)，缓存区相关数据在.git文件中
```
git add .
```
2.正式递交到分支头部
```
git commit -m '第一 次提交代码'
```
3.上传到project
```
git push orgin master
```
### 请求合并分支（将fork的项目分支合并到主分支上）
进入项目，点击pull request，在原项目主人主页会出现合并请求，主人或者是合作者（collabrator）可以选择merge request即合并请求。

## 好的参考资料
[使用说明](http://blog.csdn.net/dark00800/article/details/54571859)
[git形象使用](http://rogerdudler.github.io/git-guide/index.zh.html)
[git 各命令原理](https://my.oschina.net/xdev/blog/114383)

