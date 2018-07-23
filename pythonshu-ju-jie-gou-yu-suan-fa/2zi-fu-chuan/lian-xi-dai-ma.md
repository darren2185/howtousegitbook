### 练习代码

---

针对Python的str对象，自己实现一个replacec操作函数

```py
def replace_str(string, find_str, sub_str):
    """利用KMP求出匹配字符的位置数组"""
    _l = list(kmp(string, find_str))
    m, n, k = len(sub_str), len(string), len(find_str)

    # 字符串本身是不允许操作插入的，故先将其转换为list对象
    _str = list(string)

    if len(list(_l)) == 0:
        return False

    # 考虑插入时会导致list长度变化，故采用从尾到前的方式替换
    for i in range(len(list(_l))-1, -1, -1):
        print(i)
        print(_str[_l[i]:_l[i] + k])
        _str[_l[i]:_l[i] + k] = list(sub_str)

    return "".join(_str)
```



