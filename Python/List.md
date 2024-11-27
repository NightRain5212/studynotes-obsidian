
```
列表名 = [a1,a2,a3,...] #列表的声明
```
- 列表内的元素类型可以不相同（与C语言不同）
- 列表（[[C++/基础/数组|数组]]长度为$n$）下标索引范围 $0$ ~ $(n-1)$ 或 $-n$  ~  $-1$ (-1为倒序第一个元素)
- 索引必须在合法范围内

## 列表的部分操作

```python
L = [1,"China",3.14,[1,2],[]] #[]为空列表
L[0] == 1
L[-1] == [1,2]
L[-1][0] == 1

#列表元素增添（不产生新列表，修改了原列表）
L.append(1)  #在数组末尾添加元素
>>>print(L.append(1))
None
>>>print(L.remove(1))  #删除第一个出现的对应元素
None

# 使用pop删除元素，没有参数时默认删除最后一个，参数为对应元素的下标。
# pop的返回值是被删除的元素
>>> L.pop()
1
>>> L
['China', 3.14, [1, 2], []] 
>>> L.pop(1)
3.14
>>> L
['China', [1, 2], []]


#判断列表是否包含某元素
>>> 1 in L
True
>>>2 in L
False

a = [0,1,2,3,4,5]
#列表切片（产生新列表，不改变原列表）
>>> a[0:2] #下标索引为左闭右开区间
[0,1]
>>> a
[0, 1, 2, 3, 4, 5]

#切片的第三个参数为步长
>>>a[::2]
[0, 2, 4]

#步长为-1输出倒序列表
>>>a[::-1]
[5, 4, 3, 2, 1, 0]

#开始索引大于结束索引返回空列表
>>>a[3:1]
[]
```

## 字符串与列表的转换

```python
#字符串与列表的转换
>>> a = 'hello,world'
list(a)
['h', 'e', 'l', 'l', 'o', ',', 'w', 'o', 'r', 'l', 'd']

>>> a = list(a)
>>> s = ''.join(a)
>>> s
'hello,world'

#join的用法
#join括号内必须是字符串序列。
#'+'.join(a)  使用'+'来连接a中不同的字符串元素
>>>b = "+".join(["1","2","3"])
>>>b
'1+2+3'
```



## 栈的实现

- push：在列表的末尾添加元素
- pop：返回列表末尾的元素并删除（内置pop命令）


# list的内部结构

- 列表名是一个指针，指向一个列表（储存各个元素的指针）
- 若将列表名赋值给变量，则新变量与该列表指向同一块内存
- 真正的列表拷贝则是用分片操作(`l1 = l[:]`)

- 简单赋值
![[赋值拷贝.png]]

- 分片操作
![[分片拷贝.png]]