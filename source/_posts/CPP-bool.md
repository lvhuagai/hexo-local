---
title: C++逻辑表达式
date: 2019-01-05 18:37:05
tags: 计算机编程
src:
comments: true
---
已经2019年了，博客文章是时候写一点了，以后更新频率可能会高一些，以上。
<!-- more -->
------------

### 逻辑运算符
由数学家George Boole提出

| 说明 | 非 | 与 | 或 |
| --- | --- | --- | --- |
| 布尔代数符号 | ¬ | ∧ | ∨ |
| C++逻辑运算符 | ! | && | ll（原运算符应为两个vertical_bar符号，markdown语法原因这里无法写出） |

*在c++中，非运算优先级最高，与运算其次，或运算最低*
### 逻辑表达式
用逻辑运算符连接表达式的表达式称为逻辑表达式。逻辑表达式的结果是一个逻辑值（“真”或“假”）。
实例：`c>=75&&m>=85`
### 逻辑运算
```cpp
#include <bits/stdc++.h>
using namespace std;
int main{
	bool A,B;
	A=true;
	cout<<!A<<endl;
	//逻辑非，输出结果为0（false）
	B=false;
	if(A==true && B==true){
		cout<<"1"<<endl;
	}
	else{
		cout<<"0"<<endl;
	}
	//逻辑与，输出结果为0
	if(A==true || B==true){
		cout<<"1"<<endl;
	}
	else{
		cout<<"0"<<endl;
	}
	//逻辑或，输出结果为1
	return 0;
}
```
#### 逻辑变量
在上文代码中，出现了一个新的数据类型，这就是今天要介绍的`bool`数据类型。
```cpp
bool a,b;
//a,b两变量均为逻辑变量，又称布尔变量
```
逻辑变量只有真（1），假（0）两个值