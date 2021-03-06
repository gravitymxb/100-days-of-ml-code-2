# day2: Simple Linear Regression简单线性回归模型
## step1：Data Preprocessing数据预处理
### Importing the libraaries导入库
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
# matplotlib.pyplot,matplotlib是python上的一个2D绘图库, matplotlib下的模块pyplot是一个有命令样式的函数集合，
# matplotlib.pyplot是为我们对结果进行图像化作准备的。
```

### Imporing dataset导入数据集
```python
dataset = pd.read_csv('../GitHub clone/100-Days-Of-ML-Code/datasets/studentscores.csv')
# 读取csv文件  read_csv()方法： 从文件，url，文件型对象中加载带分隔符的数据。默认分隔符为逗号

# 这里我们需要使用pandas的iloc(区分于loc根据index来索引，iloc利用行号来索引)方法来对数据进行处理，
# 第一个参数为行号，:表示全部行，第二个参数 ：1表示截到第1列(也就是取第0列)--是一个范围
X = dataset.iloc[ : ,  : 1 ].values
Y = dataset.iloc[ : , 1 ].values
print('X:',X)
print('Y:',Y)
# X二维数组，Y一维
# 注意此处特征虽然只有学习时间这一个（一元线性回归），但是X必须是2D的（如下），否则后面的regressor.fit函数会出错。
```
### 对数据进行训练集、测试集划分
这里之前有人用sklearn库的cross_validation类即：
`from sklearn.cross_valiation import train_test_split`  
model_selection 主要提供 交叉验证 和 结果评估 的工具  
cross_validation 模块作为老版本中的模块, 拥有同样的方法, 在0.20.0版本中将会本移除, 因此尽量不要使用cross_validation 模块.  
[sklearn: model_selection的一些方法](https://blog.csdn.net/qq_39037910/article/details/73333206)
```python
from sklearn.model_selection import train_test_split
# 拆分数据，0.25作为测试集
X_train, X_test, Y_train, Y_test = train_test_split( X, Y, test_size = 1/4, random_state = 0)
```

## step2:Fitting Simple Linear Regression Model to the training set训练集使用简单线性回归模型来训练
[LinearRegression官网介绍](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html)  [中文理解](https://www.cnblogs.com/magle/p/5881170.html)

```python
from sklearn.linear_model import LinearRegression
# 使用训练集对模型进行训练
regrssor = LinearRegression()
regrssor = regrssor.fit(X_train, Y_train)
print(regressor.coef_)
print(regressor.intercept_)
# 其中coef_存放回归系数，intercept_则存放截距。
```

## step3:Predecting the Result预测结果
```python
Y_pred = regrssor.predict(X_test)
print(Y_pred)
```

## step4: Visualization可视化

### Visualizing the test results训练集结果可视化
![训练集结果可视化](https://github.com/liangju1996/100-days-of-ml-code/blob/master/day2%20train.png)

#### 散点图
```python
plt.scatter(X_train, Y_train, color = 'red')
```
#### 线图
```python
plt.plot(X_train, regrssor.predict(X_train), 'bo-')
plt.show()
```

### Visualizing the test results测试集结果可视化
![测试集结果可视化](https://github.com/liangju1996/100-days-of-ml-code/blob/master/day2%20test.png)

#### 散点图
```python
plt.scatter(X_test, Y_test, color = 'red')
```

#### 线图
```python
plt.plot(X_test, Y_pred, 'bo-')  #bo- = blue
plt.show()
```
