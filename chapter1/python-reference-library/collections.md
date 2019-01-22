# Collections

---

### [ChainMap](#chainmap)

[ChainMap]{#1}类用来管理多个映射对象，方便将多个对象当做一个来出来，比在一个字典里创建多个映射的数据，并调用每个映射的update\(\)函数快，同时也可以用来模拟嵌套作用于和模块化处理。

class collections.ChainMap\(\*map\)  
ChainMap类可将多个字典或者其他映射对象放在一起，组成一个单一的，可更新的的映射对象，若无参数，默认创建空映射对象。

```py
import collections

a = {'a': 'a', 'b': 'b'}
b = {'c': 'c', 'd': 'd'}
c = {'a': 'c', 'd': 'b'}
z = collections.ChainMap(a, b, c)

# 输出：ChainMap({'a': 'a', 'b': 'b'},{'c': 'c', 'd': 'd'},{'a': 'c', 'd': 'b'})
```

#### Maps

返回用户可更新的映射对象列表\(list对象\)

```py
import collections

a = {'a': 'a', 'b': 'b'}
b = {'c': 'c', 'd': 'd'}
c = {'a': 'c', 'd': 'b'}
z = collections.ChainMap(a, b, c)
z.maps[0]['a']='c'
print(z.maps)
# 输出：[{'a': 'c', 'b': 'b'},{'c': 'c', 'd': 'd'},{'a': 'c', 'd': 'b'}]
```

#### new\_child\(m=None\)

创建一个新的[ChainMap](#1)对象，在列表第一个元素里插入映射对象m，后面紧跟原来所有映射对象。

```py
import collections

a = {'a': 'a', 'b': 'b'}
b = {'c': 'c', 'd': 'd'}
c = {'a': 'c', 'd': 'b'}
z = collections.ChainMap(a, b, c)

xx = {'n':'m'}
z = z.new_child(xx)

# 输出ChildMap({'a': 'a', 'b': 'b'},{'c': 'c', 'd': 'd'},{'a': 'c', 'd': 'b'},{'n':'m'})
```

#### parents

返回第一个映射对象之外的所有映射对象的ChainMap对象，主要用来获取不同作用域嵌套情况，比如本地作用域、类作用域、全局作用域构造成的ChainMap就可以依次递归整个ChainMap对象，相当于ChainMap\(\*d.maps\[1:\]\)

```py
import collections

a = {'a': 'a', 'b': 'b'}
b = {'c': 'c', 'd': 'd'}
c = {'a': 'c', 'd': 'b'}
z = collections.ChainMap(a, b, c)

z.parents
# 输出 ChainMap({'c': 'c', 'd': 'd'},{'a': 'c', 'd': 'b'})
```
>小结:更新ChainMap对象可以利用maps的list属性进行修改及增删

### Counter
Counter是对字典的补充，用于追踪值出现的次数（频率统计）
```py
from collections import Counter
cnt = Counter()
for word in ['red','red','blue','green','blue','blue]:
    cnt[word] += 1
print(cnt)
# 输出:Counter({'blue':3, 'red':2, 'green':1})
```
```py
# 词频统计
import re
from collections import Counter

words = re.findall(r'\w+', open('hamlet.txt','r').read().lower())
Counter(words).most_common(10)  # 取频率前10的信息

```
> 个人猜想实现步骤：用set()对象获取所有keys,然后利用dict()对象统计词频数

Counter对象作为dict的延伸，能使用所有dict的属性和方法
### elements()
返回一个iterator对象，其元素为根据出现次数依次展开，若次数为0或者负数，则不显示出来。
```py
c=Counter(a=2,b=1,c=3)
sorted(c.elements())
# 输出['c','c','c','a','a','b']
```


