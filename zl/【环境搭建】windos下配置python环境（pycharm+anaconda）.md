@[toc]
>参考
>[关于python、pycharm、anaconda三者的关系及目录结构，一个好的博文](https://www.jianshu.com/p/eaee1fadc1e9)
# 环境
`win7-64位+pycharm2018.1+anaconda3-4.1.1`
最新版本可以到pycharm和anaconda官网下载
# pycharm
>pycharm是python使用以后比较而言比较好的IDE了，感觉无论调试还是编写代码都比较舒服，这里如何安装pycharm就不写了网上随便搜搜就行了。
>

* 一些命令
Ctrl + Space 基本的代码完成（类、方法、属性）
Ctrl + Alt + Space 类名完成
Ctrl + Shift + Enter 语句完成
Ctrl + P 参数信息（在方法中调用参数）
Ctrl + Q 快速查看文档
Shift + F1 外部文档
Ctrl + 鼠标 简介
Ctrl + F1 显示错误描述或警告信息
Alt + Insert 自动生成代码
Ctrl + O 重新方法
Ctrl + Alt + T 选中
Ctrl + / 行注释
Ctrl + Shift + / 块注释
Ctrl + W 选中增加的代码块
Ctrl + Shift + W 回到之前状态
Ctrl + Shift + ]/[ 选定代码块结束、开始
Alt + Enter 快速修正
Ctrl + Alt + L 代码格式化
Ctrl + Alt + O 优化导入
Ctrl + Alt + I 自动缩进
* 注释乱码
通过比如notepad++转为utf8 
* .pyc,.pyd
.pyc:隐藏源代码，提高运行速度，当编译.py则生成.pyc
.pyd:python动态模块，实质上是.dll文件(源代码经过编译)
* path
搜索目录只包含代码所在目录和site-package
* 去除不必要的检查
file->default settings->editor->inspection/spelling
# anaconda
>因为pycharm只是一个IDE，没有编译器，就像java除了安装eclipse等IDE还要装JDK，JDK就是java的编译器。anaconda是一个虚拟环境，处理提供编译器，还集成了各种开源库包，否则用户就要自己一个一个下载。
>
 **打开anaconda prompt**
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190212172518274.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjY0MTM5NQ==,size_16,color_FFFFFF,t_70)

* 添加Anaconda的TUNA镜像并设置搜索时显示通道地址
```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --set show_channel_urls yes
```
* 首先更新conda,因为通过conda创建新环境时要下载相关包，保证最新状态
```
conda update conda 
````
* 创建新环境（这些其实可以在IDE中设置）并查看已安装的package
```
conda create -n python35 python=3.5 anaconda
conda list -n python35
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190212172626586.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjY0MTM5NQ==,size_16,color_FFFFFF,t_70)
通过conda创建的新环境创建在envs文件夹内
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190212173221330.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjY0MTM5NQ==,size_16,color_FFFFFF,t_70)
进入刚创建的环境，比较关键的是`python.exe`编译器和`lib`包目录
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190212174046979.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjY0MTM5NQ==,size_16,color_FFFFFF,t_70)
进入到Lib中 ,这里有python自带的包, 如`日志包logging`, `异步包 concurrent`, 而所有的第三方包都放在`site-packages`文件夹里面
* 查看当前存在的环境
```
conda info --envs
```
* It looks like conda is already doing something（如果遇到conda被锁定问题）
```
conda clean --lock
```
* 新环境安装包
```
activate python35 # 进入某环境
conda install # 安装某包
conda update # 升级某包
conda update -- all#升级所有包
deactivate python35 #退出环境 
```
* 选择interpreter
因为pycharm只是一个IDE，没有自带编译器，通过anaconda新建一个自己的编译环境，其中包含了集成的科学包，以及编译器python.exe，而后项目通过这个编译器来编译，不用新建项目的时候再新建一个编译器
**default setting->project->project interpreter**
![这里写图片描述](https://img-blog.csdn.net/20180906084810528?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjY0MTM5NQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
  选择编译器
* 新建一个project时
![这里写图片描述](https://img-blog.csdn.net/20180906084850531?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjY0MTM5NQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
 选择已存在的编译器
![这里写图片描述](https://img-blog.csdn.net/20180906084907474?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjY0MTM5NQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
选择之前创建的编译器
# python实用库
* python 语法好的整理网站
http://www.runoob.com/python/python-tutorial.html
* matplotlib
 * 解决闪退
    python2.*后面加上：raw_input()
     python3.*后面加上：input()
* pandas
* scrapy
* tensorflow
中文手册
http://www.tensorfly.cn/tfdoc/api_docs/index.html
* 解决出现无编译的warning
```
import os
os.environ['TF_CPP_MIN_LOG_LEVEL']='2'
```
* opencv
官网直接下载opencv，Browse Files at SourceForge.net，下载合适的版本，直接执行exe文件，安装完成后，到C:\python\opencv\build\python\2.7\x64选中cv2.pyd(64还是86根据自己版本)，复制到Anaconda3\Lib\site-packages。


----------
* [Doraengineer's blog说明](https://blog.csdn.net/weixin_42641395/article/details/82558190)

