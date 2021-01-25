---
title: 大数据课程设计-spark环境搭建以及实现决策树学习
date: 2020-09-27 09:55:50
tags: 工作
---
学期初大数据课程老师要求仿照林子雨老师的教材使用spark编写程序，本想随便画两张图草草了事，但最后还是认真地做了。
有趣的是答辩的时候，有四组的作品和林子雨老师教材的例子一模一样，这大概就是糊弄学的典范吧。
# 大数据课程设计-spark环境搭建以及实现决策树学习
## 环境配置
使用manjaro、java 1.8、hadoop 2.9.2、 python 3.8
以及安装了mysql，此处不作展示
![Python和Spark版本信息](https://i.loli.net/2020/10/05/pNY51TcBw49uHol.png "环境信息.1")
![JDK和Hadoop版本信息](https://i.loli.net/2020/10/05/91tSrjXaxN6zOpA.png "环境信息.2")
spark可以独立于hadoop运行（hadoop配置是真的麻烦），并且本课设采用的是pyspark编程，pyspark需要python3.x以上的版本
## 数据集
![数据集](https://i.loli.net/2020/10/05/qLHkJr5EVn32Yly.png "数据集.1")
数据集采用国民经济核算季度数据，CPI为国家人均消费指数，指数越高说明消费水平越高，接下来将使用pyspark的ml模块的决策树模型进行训练和测试

## 数据处理
```
"""
    导入必要的模块
"""
from pyspark.sql import SparkSession
from pyspark.ml.feature import VectorAssembler
from pyspark.ml.regression import DecisionTreeRegressor
from pyspark.ml.evaluation import RegressionEvaluator
```
SparkSession 是 spark2.x 引入的新概念，SparkSession 为用户提供统一的切入点，字面理解是创建会话，或者连接 spark
VectorAssembler 将多列数据转换为单列的向量列并统一命名，完成特征向量提取
DecisionTreeRegressor 为决策树模型模块，包含了初始化训练测试等方法
RegressionEvaluator 用于对模型进行评估

```
spark = SparkSession.builder.appName('learn_regression').master('local[1]').getOrCreate()
dataset_path = './data/datat.csv'
df = spark.read.csv(dataset_path)
```
读取数据集并且创建本地spark会话
```
  df = df.withColumn('_c1',df._c1.astype("float"))
  df = df.withColumn('_c2',df._c2.astype("float"))
  df = df.withColumn('_c3',df._c3.astype("float"))
  df = df.withColumn('_c4',df._c4.astype("float"))
  df = df.withColumn('_c5',df._c5.astype("float"))
  df = df.withColumn('_c6',df._c6.astype("float"))
  df = df.withColumn('_c7',df._c7.astype("float"))
  df = df.withColumn('_c8',df._c8.astype("float"))
  df = df.withColumn('_c9',df._c9.astype("float"))
  df = df.withColumn('_c10',df._c10.astype("float"))
  df = df.withColumn('_c11',df._c11.astype("float"))
  df = df.withColumn('_c12',df._c12.astype("float"))
  df = df.withColumn('_c13',df._c13.astype("float"))
  df = df.withColumn('_c14',df._c14.astype("float"))
  df.show()
```
将数据的每一列转换成float浮点数类型
```
def feature_converter(df):
    """
        使用feature模块的VectorAssembler将特征值提取并合并
    """
    vecAss = VectorAssembler(inputCols = df.columns[1:], outputCol= 'features')
    df_va = vecAss.transform(df)
    return df_va
```
定义一个特征提取函数，将使用VectorAssembler提取特征值并合并重命名为features
```
train_data, test_data = feature_converter(df).select('features','_c14').randomSplit([7.0,3.0], 101)
```
此处C_14为数据集中的CPI，特征提取完成后按照7-3划分训练集和测试集
## 训练与评估
```
# 创建一个决策树对象
dt = DecisionTreeRegressor(maxDepth=5, varianceCol="variance", labelCol="_c14")
# 使用训练集数据 进行训练
dt_model = dt.fit(train_data)
```
使用ml模块的随机森林模型进行训练
```
dt_evaluator = RegressionEvaluator(labelCol='_c14',metricName="rmse",predictionCol='prediction')
rmse = dt_evaluator.evaluate(result)
print("均方根的误差为：",rmse)
```
对模型进行评估，结果如下
![评估结果](https://i.loli.net/2020/10/05/z4XNBOV1PhD3wC6.png "评估结果")
