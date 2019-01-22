# Collections

---

### ChainMap[1]

ChainMap类用来管理多个映射对象，方便将多个对象当做一个来出来，比在一个字典里创建多个映射的数据，并调用每个映射的update\(\)函数快，同时也可以用来模拟嵌套作用于和模块化处理。

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

创建一个新的ChainMap对象，在列表第一个元素里插入映射对象m，后面紧跟原来所有映射对象。

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
###

