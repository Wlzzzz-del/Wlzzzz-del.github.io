---
title: networkx复杂网络基本操作
date: 2020-09-27 12:41:04
tags: 工作
---
从寒假开始到疫情结束一直在帮研究生搞复杂网络的算法，因此学习了networkx用于写算法，在这篇博文下整理一些networkx的基本操作
# networkx基本操作
## 导入数据集
导入.gml格式的数据集
```
G.read_gml()
```
导入.txt格式的数据集
```
G.read_edgelist()
```
导入karate_club数据集（networkx自带）
```
G.karate_club_graph()
```

## 点和边的操作
输出点的数量
```
G.number_of_nodes()
```
输出边的数量
```
G.number_of_edges()
```
输出全部点的信息
```
G.nodes()
```
输出全部边的信息
```
G.edges()
```
在图中添加一个点
```
G.add_node(34)
```
在图中添加一条边
```
G.add_edge(1,3)
```
输出某个点的邻居节点
```
G[34]
```
使用遍历输出所有点的邻居数量
```
for i in G.nodes():
  print(i,'的数量为',len(G[i]))
```
## 画图操作
networkx画图操作依托于matplotlib，因此matplotlib设置的参数对nx.draw()都有效
```
from matplotlib import pyplot as pyplot
plt.figure(figsize=(10,8))# 定义图片的大小
nx.draw(G)
plt.show()
```
如下图画出了karate的拓扑图
![karate](http://i1.fuimg.com/727535/bc6dfba58eb1265a.png "karate拓扑结构.1")
```
nx.draw(G,node_color='r',edge_color='b')#指定点和边的颜色
```
![karate](http://i1.fuimg.com/727535/40e48e4e44925b81.png "karate拓扑结构.2")

```
# 使用Kernighan–Lin算法将图划分为两个块
a=kernighan_lin_bisection(G)# 运行算法
pos = nx.spring_layout(G)# 对节点布局进行美化
# 分别画出两组社区的节点分布
nx.draw(G,pos = pos, nodelist = a[0], node_color = 'blue',node_size=100)
nx.draw(G,pos = pos, nodelist = a[1], node_color = 'red',node_size=100)
```
![karate](http://i2.tiimg.com/727535/f7135e3a3a576499.png "karate拓扑结构.3")

## 生成其他特殊图
```
G = nx.scale_free_graph(100)# 生成无标度网络
H=nx.watts_strogatz_graph(50,5,0.3)# 生成小世界
```

## 导出到.gml格式
```
nx.write_gml(G,'./9.txt')
```

## 其他详细方法参考networkx文档
[networkx文档](https://www.osgeo.cn/networkx/ "networkx文档")
