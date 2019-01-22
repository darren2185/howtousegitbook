# Collection

---

#### ChainMap

ChainMap类用来管理多个映射对象，方便将多个对象当做一个来出来，比在一个字典里创建多个映射的数据，并调用每个映射的update\(\)函数快，同时也可以用来模拟嵌套作用于和模块化处理。

class collections.ChainMap\(\*map\)  
ChainMap类可将多个字典或者其他映射对象放在一起，组成一个单一的，可更新的的映射对象，若无参数，默认创建空映射对象。
```py
import collections

a = {'a': 'a', 'b': 'b'}
b = {'c': 'c', 'd': 'd'}
c = {'a': 'c', 'd': 'b'}
z = collections.ChainMap(a, b, c)

# ChainMap({'a': 'a', 'b': 'b'},{'c': 'c', 'd': 'd'},{'a': 'c', 'd': 'b'})
```
#### Maps
返回用户可更新的映射对象列表(list对象)
```py
import collections

a = {'a': 'a', 'b': 'b'}
b = {'c': 'c', 'd': 'd'}
c = {'a': 'c', 'd': 'b'}
z = collections.ChainMap(a, b, c)

print(z.maps)
# [{'a': 'a', 'b': 'b'},{'c': 'c', 'd': 'd'},{'a': 'c', 'd': 'b'}]
```




