# 概述
之前做数据处理用的比较多的是Matlab,因为环境配置简单，不像c++,java在配置上存在一下一些问题
* 编译器会生成工程文件，这些工程能文件通常较大，在上传例如`github`时需要剔除较大的工程文件例如`.proj`等是c++、java创建工程时生成的一些文件，而分享只需分享`.cpp`,`.h`,`.java`等实际功能代码文件，其他人需要将这些重新在编译器中进行导入，配置，运行含main函数的`.cpp`
* 在引用其他`.cpp`中的函数时需要写头文件`.h`，在头文件里写函数原型，在主`.cpp`中`include  .h`,或者在主`cpp`中开头写所有需要引用函数的函数原型
* 一个工程里只能存在一个main函数，当运行其他功能时需要将冲突的功能注释掉
* 经常要配置连接一些打包的函数例如`.dll`,`.lib`,很多开源包也是以打包的形式发布，无法看到源代码。
**因此c++、java等基础语言适合做大型实用性工程 ，优化等方面技术，但对于代码分享复现存在一定门槛**

而matlab在基本数据处理方面有一下一些优点
* .m文件可以独立运行不需要复杂配置，引用其他.m中的函数只需确保放在统一文件夹下，或者添加文件夹路径
* IDE不需要复杂的配置，.m文件即开即用
* 后台变量数据查看较为方便，不以缓存的形式消亡

而python在matlab基础上又具备了数据处理方面的一些优势
* matlab具备的优点python都具备
* 数据处理方面的科学包比较丰富且比较系统
* 有例如anaconda的包管理工具

以下整理一些python关于数据处理相关的开源库
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190214100655438.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjY0MTM5NQ==,size_16,color_FFFFFF,t_70)
# 参考资料
## 官方文档
https://scipy.org/
官方文档里面分里几个层次的指南
* developer guide 开发者指南
* reference guide 用户参考指南（介绍得更为详细）
* user guide 用户指南（偏重用户使用）
## 好的学习笔记（Lecture Note）
http://scipy-lectures.org/
# 好的中文手册，
* Numpy https://www.numpy.org.cn/
* Pandas https://www.pypandas.cn/ 
  pandas API速查 https://www.jianshu.com/p/a77b0bc736f2 翻译自 (https://www.dataquest.io/blog/pandas-cheat-sheet/ )
* Matplotlib http://reverland.org/python/2012/09/07/matplotlib-tutorial/
* keras https://keras.io/zh/
* Scikit-Learn http://sklearn.apachecn.org/#/* 

----------
* [Doraengineer's blog说明](https://blog.csdn.net/weixin_42641395/article/details/82558190)
