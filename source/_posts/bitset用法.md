---
title: C++ bitset
date: 2020-10-16 09:55:42
tags: 学习
---
C++ 的 bitset 在 bitset 头文件中，它是一种类似数组的结构，它的每一个元素只能是0或者1,每个元素仅占用1bit空间
# 引入
```C++
#include <bits/stdc++.h>
```

# 构造函数
```C++
bitset<4> bitset1;//无参数构造，长度为4,默认每一位为0
bitset<8> bitset2(12);//长度为8，二进制保存，前面用0补充
```
```C++
string s = "100101"
bitset<10> bitset3(s);//长度为10,前面用0补充
```
```C++
char s2[]="10101"
bitset<13> bitset4(s2);//长度为13，前面用0补充
```
```C++
cout<<bitset1<<endl;//0000
cout<<bitset2<<endl;//00001100
cout<<bitset3<<endl;//0000100101
cout<<bitset4<<endl;//0000000010101
```

注意：  
使用字符串构造时，字符串只能包含'0'或者'1'，否则会抛出异常。  
构造时，需要在<>中声明bitset的大小(即size)。  
在进行有参构造时，若参数的二进制表示比bitset的size小，则在前面用0补充(如上面的例子);若比bitsize大，参数为整数时取后面部分，参数为字符串时取前面部分(如下例子):

```C++
bitset<2> bitset1(12);//12的二进制为1100（长度为4），但bitset1的size=2,只能取后面部分，即00

string s = "100101";
bitset<4> bitset2(s);//s的size=6,只取前面的部分，即1001

char s2[]="11101"
bitset<4> bitset3(s2);//与bitset2同理，只取前面部分，即1110

cout<<bitset1<<endl; //00
cout<<bitset2<<endl; //1001
cout<<bitset3<<endl; //1110
```


# 可用的操作符
bitset 对于二进制有位操作符，具体如下

```C++
bitset<4> foo (string("1001"));
bitset<4> bar (string("0011"));

cout << (foo^=bar) <<endl; //1010（foo对bar按位异或后赋值给foo）
cout << (foo&=bar) << endl;       // 0010 (按位与后赋值给foo)
cout << (foo|=bar) << endl;       // 0011 (按位或后赋值给foo)

cout << (foo<<=2) << endl;        // 1100 (左移２位，低位补０，有自身赋值)
cout << (foo>>=1) << endl;        // 0110 (右移１位，高位补０，有自身赋值)

cout << (~bar) << endl;           // 1100 (按位取反)
cout << (bar<<1) << endl;         // 0110 (左移，不赋值)
cout << (bar>>1) << endl;         // 0001 (右移，不赋值)

cout << (foo==bar) << endl;       // false (0110==0011为false)
cout << (foo!=bar) << endl;       // true  (0110!=0011为true)

cout << (foo&bar) << endl;        // 0010 (按位与，不赋值)
cout << (foo|bar) << endl;        // 0111 (按位或，不赋值)
cout << (foo^bar) << endl;        // 0101 (按位异或，不赋值)
```
# 访问
bitset类似数组，使用[]符号进行访问，最低位为0：
```C++
bitset<4> foo ("1011");

cout<< foo[0] <<endl; //1
cout<< foo[1] <<endl; //0
```
同样可以使用这种方式进行赋值

# 函数

| 函数  |    功能                     |
| ----  |    ----                     |
| count |    求bitset中1的位数        |
| size  |    求bitset大小             |
| test  |    检查元素是0还是1         |
| any   |    检查bitset中是否有1      |
| none  |    检查bitset中是否没有1    |
| all   |    检查bitset中是否全部为1  |
| flip  |    将bitset中的每一位都取反 |
| set   |    将bitset中每一位都置为1  |
| reset |    将bitset每一位置为0      |

flip,set,reset具体如下

```C++
bitset<8> foo ("10011011");

cout << foo.flip(2) << endl;　　//10011111　　（flip函数传参数时，用于将参数位取反，本行代码将foo下标２处"反转"，即０变１，１变０
cout << foo.flip() << endl;　　 //01100000　　（flip函数不指定参数时，将bitset每一位全部取反

cout << foo.set() << endl;　　　　//11111111　　（set函数不指定参数时，将bitset的每一位全部置为１
cout << foo.set(3,0) << endl;　　//11110111　　（set函数指定两位参数时，将第一参数位的元素置为第二参数的值，本行对foo的操作相当于foo[3]=0
cout << foo.set(3) << endl;　　  //11111111　　（set函数只有一个参数时，将参数下标处置为１

cout << foo.reset(4) << endl;　　//11101111　　（reset函数传一个参数时将参数下标处置为０
cout << foo.reset() << endl;　　 //00000000　　（reset函数不传参数时将bitset的每一位全部置为０
```
