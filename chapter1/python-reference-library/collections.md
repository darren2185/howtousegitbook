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
#### elements()
返回一个iterator对象，其元素为根据出现次数依次展开，若次数为0或者负数，则不显示出来。
```py
c=Counter(a=2,b=1,c=3)
sorted(c.elements())
# 输出['c','c','c','a','a','b']
```
#### most_common([n])
返回出现前n次元素列表，如果n缺省，则显示所有，按统计次数从大到小。
```py
Counter('abracadabra').most_common(3)
[('a', 5),('r',2),('b',2)]
```
### substract([iterable-or-mapping])
相当于dict.update()更新
```py
c = Counter(a=4, b=2, c=0, d=-2)
d = Counter(a=1, b=2, c=3, d=4)
c.substract(d)
c
# Counter({'a':3, 'b':0 , 'c':-3, 'd': -6})
```
### deque()
###deque([iterable[,maxlen]])
初始化双端队列对象，返回一个从左至右具有迭代性的双端队列，如果iterable为空则初始为空的deque对象。如果maxlen为空，则deque对象空间为无限，否则在操作deque时，需要考虑容积个数，空间已满，再添加元素，从添加侧的相反一段，排挤出一个元素。deque是double-ended queue的缩写，主要用来支持线程安全thread-safe, 内存添加或删除。
> append(x) 右侧添加
> appednleft(x) 左侧添加
> clear() 清楚deque中的所有元素
> copy() 浅复制
> count(x)  统计满足元素为x的个数
> extend(iterable) 在右侧扩展deque
> extendleft(iterable)在左侧扩展deque,将会颠倒iterable的顺序
> index(x[,start[,stop]]]) 返回x在deque中的位置，返回第一个出现的位置或者raise ValueError if not found
> insert(i, x) 在i位置插入x
> pop() right side
> popleft()
> remove(value) 
> reverse()
> rotate(n=1) rotate 1步，n为+，相当于d.appendleft(d.pop())，n为1，相当于d.append(d.popleft())
> maxlen deque的最大容纳值

### defaultdict()

```py
def default_example1():
    s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
    dd ={}
    for k, v in s:
        dd.setdefault(k, [])
        dd[k].append(v)

    print(sorted(dd.items()))


def default_example2():
    s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
    dd = defaultdict(list)
    for k, v in s:
        dd[k].append(v)

    print(sorted(dd.items()))
```

































