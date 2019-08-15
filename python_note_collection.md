# list & tuple
## list列表——有序集合
- `len(listname)` 获取list元素个数
- `IndexError` 越界错误
- `-1` 作为索引时，获取list最后一个元素
- `listname.append()` 尾部添加
- `listname.insert(index,content)` 向指定位置添加元素
- `listname.pop(<index>)` 参数为空删除末尾元素、不为空删除索引位置元素
- `listname[index] = content` 直接赋值指定索引元素，替换元素值
- list内数据类型可以不同
- list可包含list形成二维数组
## tuple 元组——有序列表
> 一旦初始化就不能修改——更加安全
- 可以定义空的tuple → `t=()`
- 定义只有一个元素的元组必须使用 → `t=(1,)`
---
# 循环
- for循环
    ```
    for x in list|tuplename
    ```
    `range()` 函数生成一个整数序列
- while循环
  ```
  while 条件:
        .....
    ```
- break 跳出循环
- continue 跳过此次循环，进入下一轮循环
---
# dict和set
## dict 字典(dictionary)——类似于`map`
- `dictname = {'key':value,'key1':value...}`
- 取用key值 `dictname['key']`
- 键值配对，一键一值
- 避免`key`不存在，使用：`‘key’ in dictname` 判断是否存在
- `dictname.get('key'[,vlaue])` 也可用于判断是否存在`key`
- 删除key键值对：`dictname.pop(key)`
## set 只存key不存value——与Java中setlist类似，无重复值
- 创建`set`需要提供一个`list`作为输入集合
- 添加元素 `setname.add(key)`
- 删除元素 `setname.remove(key)`
- 两个set使用 `set1 & set2` 取交集，使用 `set1 | set2` 取并集
---
# 不可变对象
> python的函数参数传递，既不是值传递，也不是引用传递。它的传递方式是”传对象“。函数参数在传递的过程中，将整个对象传入。
1. 对可变对象的修改在函数外部以及内部都可见；
2. 对于不可变对象，由于不能真正的修改，往往是创建一个新的对象，然后通过赋值来实现。，所以，外部是不可见的。
> 修改一个不可变对象的时候，会创建一个新的对象，然后指过去。

具体参考：https://www.jianshu.com/p/0d5028d67f92?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation
---
###### 修改时间：2019年8月15日10点43分
---
---
