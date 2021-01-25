---
title: map 与 unordered_map的基本用法及区别
date: 2020-12-30 10:55:42
tags: 学习
---
# map
## 特性
+ 所有元素根据元素的键值key自动排序
+ 每个元素都是<key,value>的键值对
+ 不允许有键值相同的元素
+ key不能修改，但可以通过key修改与其对应的value
+ 可以删除与value对应的键值key，重新插入以达到修改的目的
## 优点
+ 有序性，这是map结构最大的优点，可以简化很多操作
+ 红黑树，内部实现一个红黑树使得map很多操作可以在$log_n$复杂度下就可以实现，效率非常高
## 缺点
+ 空间占用率高，map内部实现了红黑树，虽然提高了运行效率，但是每个结点都需要额外保存父节点、孩子节点和红黑性质，使得每个结点都占用大量的空间

## 作用场景
+ 字典
+ 统计出现次数
##常用操作
```C++
//初始化和插入
unordered_map<int, string> mymap = {{4, "张大"},{5, "李五"}};//使用{}赋值
myMap[2] = "李四";//使用[]进行单个插入，若已经存在键值2,则赋值修改，若无则插入
myMap.insert(pair<int, string>(3, "陈二"));//使用insert和pair插入


//遍历输出+迭代器使用
auto iter= myMap.begin();//auto自动识别迭代器类型为unordered_map<int, string>
while(iter!=myMap.end())
{
  cout<< iter->first <<"," << iter->second <<endl;
	++iter;
}

//查找元素并输出+迭代器的使用
auto iterator = myMap.find(2);//find返回一个指向2的迭代器
if((iterator != myMap.end())
				cout<< endl << iterator->first <<"," <<iterator->second<<endl;
system("pause");
return 0;
```

# unordered_map
## 优点
+ 内部实现了Hash_table，因此查找速度非常快
## 缺点
+ 建立Hash_table耗费时间
## 作用场景
+ 查找问题  

## 常用操作
与map类似
