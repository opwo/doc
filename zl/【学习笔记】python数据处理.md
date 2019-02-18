# numpy
> python并没有提供数组功能，虽然列表可以完成基本的数组功能，但它不是真正的数组，且数据量较大时，列表速度会非常慢，因此，Numpy提供了真正的数组功能，使python有了matlab的味道，以及对数据进行快速处理的函数。同时Numpy是很多高级的拓展库的依赖库。

## 引用
```
import numpy as np #一般以np作为numpy的别名
```
## 数组
 * 创建数组
```
a = np.array([2, 0, 1, 5]) #创建数组
```
 * 引用
```
a[:3] #引用前三个数字（切片）
```
*  将data转换为bool类型
```
data == u'好' # 数组转换为bool类型
data[data == u'是']  #用布尔类型数组来取data的值
```

 * 二维数组
```
b= np.array([[1, 2, 3], [4, 5, 6]]) #创建二维数组
```
## 生成自变量
```
x = np.linspace(0, 10, 1000) #作图的变量自变量
```
## 建立范围
```
np.arange(1, 9, 0.25)
```
## 打乱数据
```
from numpy.random import shuffle #引入随机函数
shuffle(data) #随机打乱数据
data_train = data[:int(0.8*len(data)), :] #选取前80%为训练数据
data_test = data[int(0.8*len(data)):, :] #选取前20%为测试数据

```
# scripy
>Numpy只是让python有了matlab的味道，虽然提供了多维数组功能，但只是一般数组，并不是矩阵。当数组相乘，只是对应元素相乘，而不是矩阵乘法。Scripy提供了真正的矩阵，及大量基于矩阵运算的对象与函数。
* 读取mat数据
```
from scipy.io import loadmat #mat是MATLAB专用格式，需要用loadmat读取它
mat = loadmat(inputfile)
signal = mat['leleccum'][0]
```

# pandas
>pandas是python下强大的数据分析和探索工具，最初被作为金融数据分析工具而开发出来。支持类似于SQL的数据增、删、改，并带有丰富的数据处理函数。

## 与EXCEL交互
>Pandas还不能读写Excel文件，需安装xlrd(读)，xlwt(写)库才能支持Excel的读写。
* 读取表格，文本
```
data = pd.read_csv(datafile,encoding='utf-8')#表格里有汉字
pd.read_excel('data.xls') #读取Excel文件，创建DataFrame。
pd.read_csv('data.csv', encoding = 'utf-8') #读取文本格式的数据，一般用encoding指定编码。
```
* 读取表格，已某一列为索引项
```
data = pd.read_excel(catering_sale, index_col = u'日期') #读取数据，指定“日期”列为索引列

```
## 基本概念
* Series 序列
相当于一维数组
* DataFrame 二维表格
类似二维数组，每一列都是一个Series
* Index对象
为了定位Series中的元素，每个Series都会带一个对应Index，类似于SQL中的主键。DataFrame相当于多个带有同样Index的Series的组合，每个Series都带有唯一的表头，来标识不同的Series。
## 操作
* 创建序列
```
s = pd.Series([1,2,3], index=['a', 'b', 'c'])
```
* 创建表格
```
d = pd.DataFrame([[1, 2, 3], [4, 5, 6]], columns = ['a', 'b', 'c']) #创建一个表
d2 = pd.DataFrame(s) #也可以用已有的序列来创建表格
```
* 对行列操作
```
data['w']#w列，返回序列
data[['w']]#w列，返回dataframe
data[1:3]#取2到3行(前闭后开)
data.iat[1,1]#取第二行第二列
data[i][j] #第i列第j行(注意数组的表示)（可以用来通过判定取某些数据）
data[int(len(data)*p):,:]#..行..列
data.loc['a',['w','x']]#返回a行，w,x列
data.head()#返回前几行
data.tail()#返回后几行
data.iloc[-1]#最后一行，返回序列
data.iloc[-1:]#最后一行，返回dataframe
```
* 保存表格

```
pd.DataFrame(cm_train, index = range(1, 6), columns = range(1, 6))# 改变行列标题
```
* 保存结果
```
data_processed.to_excel(transformeddata, index = False)
```

* 标准化
```
data_zs = 1.0*(data - data.mean())/data.std() #数据标准化
```
* 计算相关系数
```
a=data.corr() #相关系数矩阵，即给出了任意两款菜式之间的相关系数
b=data.corr()[u'百合酱蒸凤爪'] #只显示“百合酱蒸凤爪”与其他菜式的相关系数
c=data[u'百合酱蒸凤爪'].corr(data[u'翡翠蒸香茜饺']) #计算“百合酱蒸凤爪”与“翡翠蒸香茜饺”的相关系数
```
* 正则化（数据按列）
```
(data - data.min())/(data.max() - data.min()) #最小-最大规范化
(data - data.mean())/data.std() #零-均值规范化
data/10**np.ceil(np.log10(data.abs().max())) #小数定标规范化
```
* 计算基本统计量（count   mean  std     min     25%   50%   75%   max   ）
```
statistics = data.describe()
```
* 计算极差，变异系数，四分位间距
```
statistics.loc['range'] = statistics.loc['max']-statistics.loc['min'] #极差
statistics.loc['var'] = statistics.loc['std']/statistics.loc['mean'] #变异系数
statistics.loc['dis'] = statistics.loc['75%']-statistics.loc['25%'] #四分位数间距
```
* 相邻做差分
```
  d = data[u'发生时间'].diff() > ts #相邻时间作差分，比较是否大于阈值
```
# matplotlib
>对于python来说，Matplot是最著名的绘图库，主要用于二维绘图，也可进行简单的三维绘图，提供了一套和matlab相似但更为丰富的命令。
* 设置图像大小，x,y轴名称，标题，显示范围，显示图例
```
plt.figure(figsize = (8, 4)) #建立图像,设置图像大小
plt.xlabel('Time(s) ') # x轴名称
plt.ylabel('Volt') # y轴名称
plt.title('A Simple Example') #标题
plt.ylim(0, 2.2) #显示的y轴范围
plt.legend() #显示图例
plt.show() #显示作图结果
```
 * 做点
```
plt.plot(x,y,label = '$\sin x+1$', color = 'red', linewidth = 2) #作图，设置标签、线条颜色、线条大小
plt.plot(x, z, 'b--', label = '$\cos x^2+1$')  #作图，设置标签、线条类型
```

* 箱图
```
import matplotlib.pyplot as plt #导入图像库
plt.rcParams['font.sans-serif'] = ['SimHei'] #用来正常显示中文标签
plt.rcParams['axes.unicode_minus'] = False #用来正常显示负号

plt.figure() #建立图像
p = data.boxplot(return_type='dict') #画箱线图，直接使用DataFrame的方法

```
* 添加点注释
```
x = p['fliers'][0].get_xdata() # 'flies'即为异常值的标签
y = p['fliers'][0].get_ydata()
y.sort() #从小到大排序，该方法直接改变原对象

for i in range(len(x)):
  if i>0:
    plt.annotate(y[i], xy = (x[i],y[i]), xytext=(x[i]+0.05 -0.8/(y[i]-y[i-1]),y[i]))
  else:
    plt.annotate(y[i], xy = (x[i],y[i]), xytext=(x[i]+0.08,y[i]))

```
```
plt.annotate(format(p[6], '.4%'), xy = (6, p[6]), xytext=(6*0.9, p[6]*0.9), arrowprops=dict(arrowstyle="->", connectionstyle="arc3,rad=.2")) #添加注释，即85%处的标记。这里包括了指定箭头样式。
```
* 做柱状图
```
data.plot(kind='bar')
```
* 画第二个y轴
```
p.plot(color = 'r', secondary_y = True, style = '-o',linewidth = 2)
```
* 自定义作图函数
```
def density_plot(data): #自定义作图函数
  import matplotlib.pyplot as plt
  plt.rcParams['font.sans-serif'] = ['SimHei'] #用来正常显示中文标签
  plt.rcParams['axes.unicode_minus'] = False #用来正常显示负号
  p = data.plot(kind='kde', linewidth = 2, subplots = True, sharex = False)
  [p[i].set_ylabel(u'密度') for i in range(k)]
  plt.legend()
  return plt
```
# sklearn
>Scikit-Learn是python下强大的机器学习工具包，提供了完善的机器学习工具箱，包括数据预处理、分类、回归、聚类、预测和模型分析等。依赖于Numpy,Scripy,Matplotlib.
* 逻辑回归
```
rom sklearn.linear_model import LogisticRegression as LR
from sklearn.linear_model import RandomizedLogisticRegression as RLR 
rlr = RLR() #建立随机逻辑回归模型，筛选变量
rlr.fit(x, y) #训练模型
rlr.get_support() #获取特征筛选结果，也可以通过.scores_方法获取各个特征的分数
print(u'通过随机逻辑回归模型筛选特征结束。')
print(u'有效特征为：%s' % ','.join(data.columns[rlr.get_support()]))
x = data[data.columns[rlr.get_support()]].as_matrix() #筛选好特征

lr = LR() #建立逻辑回归模型
lr.fit(x, y) #用筛选后的特征数据来训练模型
print(u'逻辑回归模型训练结束。')
print(u'模型的平均正确率为：%s' % lr.score(x, y)) #给出模型的平均正确率，本例为81.4%
```

* pca
```
from sklearn.decomposition import PCA

pca = PCA()
b=pca.fit(data)
a=pca.components_ #返回模型的各个特征向量
pca.explained_variance_ratio_ #返回各个成分各自的方差百分比
```
# svm
```
from sklearn import svm
model = svm.SVC()
model.fit(x_train, y_train)
import pickle # 保存模型
pickle.dump(model, open('../tmp/svm.model', 'wb'))
```



# keras
>虽然Scikit-Learn足够强大，但是它并没有包含一种强大的模型——人工神经网络。Keras并非简单的神经网络库，而是基于Theano的强大的深度学习库，利用它不仅仅可以搭建普通的神经网络，还可以搭建各种深度学习模型，如自编码器、循环神经网络、递归神经网络、卷积神经网络等。依赖于Numpy、Scripy、Theano。
## Theano
>Theano也是python的一个库用来定义、优化和高效解决多维数组数据对应数学表达式的模拟估计问题，
* windos
先安装MinGW(windos下的GCC和G++),再安装Theano(提前装好Numpy等依赖库)，最后安装Keras。实现Gpu加速，还需安装和配置CUDA。然而，在windos下的Keras速度会大打折扣。因此想在神经网络和深度学习方面进行研究建议在Linux环境下进行。
* linux
需要c++编译器，Linux下是自带的，在Linux下安装Theano和Keras只需要下载源代码，然后`python setup.py install`安装就行。
## 操作
 * 建立模型
```
from keras.models import Sequential
from keras.layers.core import Dense, Dropout, Activation

model = Sequential() #建立模型
model.add(Dense(11, input_shape = 17))
# model.add(Dense(11, 17)) #添加输入层、隐藏层的连接
model.add(Activation('relu')) #以Relu函数为激活函数
model.add(Dense(17, 10)) #添加隐藏层、隐藏层的连接
model.add(Activation('relu')) #以Relu函数为激活函数
model.add(Dense(10, 1)) #添加隐藏层、输出层的连接
model.add(Activation('sigmoid')) #以sigmoid函数为激活函数
#编译模型，损失函数为binary_crossentropy，用adam法求解
model.compile(loss='binary_crossentropy', optimizer='adam', class_mode="binary") 
```
 * 训练
```
model.fit(x_train, y_train, nb_epoch = 100, batch_size = 1) #训练模型
model.save_weights('../tmp/net.model') #保存模型参数
```
* 预测
```
r = pd.DataFrame(model.predict_classes(x_test), columns = [u'预测结果'])
pd.concat([data_test.iloc[:,:5], r], axis = 1).to_excel(testoutputfile)

```


----------
* [Doraengineer's blog说明](https://blog.csdn.net/weixin_42641395/article/details/82558190)

