---
title: Coursera机器学习案例研究
date: 2017-10-17 21:29:48
tags: [machine learning,pyhton,Graphlab]
categories: 小橙子的笔记
---

# Coursera机器学习案例研究

## Graphlab 库介绍

### 初始化

```py
import graphlab
graphlab.product_key.set_product_key('your product key here')
graphlab.set_runtime_config('GRAPHLAB_DEFAULT_NUM_PYLAMBDA_WORKERS', 4)
```

### 读取数据

```py
sf = graphlab.SFrame('people-example.csv')
```

可读取的数据类型有csv,dict,list等

### 显示前几条数据

```py
sf.head()
```

### 显示后几条数据

```py
sf.tail()
```

### 设置画布在当前notebook中展示

```py
graphlab.canvas.set_target('ipynb')
```

### 显示数据

```py
sf.show()
sf.show(view='Categorical')#参数可选
sf.show(view='Scatter Plot',x='x',y='y')#根据x,y绘制散点图
```

### 针对列进行操作

```py
sf['index']=sf['index']+2
sf['add_column']=sf['index']*2
```

### 对每一列应用函数

```py
def fun(x):
	if x>=2:
		return 1
	else:
		return 0
		
sf['age'].apply(fun)
```

### 切分数据，分成训练集、测试集

```py
train_data,test_data = sf.random_split(.8,seed=0)
```

### 训练模型

#### 训练线性回归模型

```py
linear_model = graphlab.linear_regression.create(train_data,target='欲求的变量',features=['使用的特征1'，'使用的特征2'],validation_set=None)
```

#### 得到模型的各个参数

```py
linear_model.get('coefficients')
#得到模型各个特征的系数，如果特征的值类型为string类型，会使用dummy coding进行编码，最终得到n-1个dummy coefficient
```

#### 训练logistic regression分类模型

```pyth
lr_model = graphlab.logistic_classifier.create(train_data,target='sentiment',features=[],validation_set=test_data)
```

### 评估模型

```py
#linear regression model 的评估
linear_model.evaluate(test_data)
#{'max_error': 4143550.8825285914, 'rmse': 255191.02870527367}
#rmse为标准差，mse为方差


#logistic classifier model的评估
lr_model.evaluate(test_data,metric='roc_curve')
lr_model.show(view='Evaluation')
```

### 应用模型预测数据

```py
#线性回归模型预测数据
linear_model.predict(test_data[0])

#logistic regression模型预测数据的分类,可以指定输出类型为概率
lr_model.predict(test_data,output_type='probability')
```

