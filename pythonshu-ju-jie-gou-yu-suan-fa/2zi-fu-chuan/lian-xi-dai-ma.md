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

根据分隔符找出最大子串

1.找出分割符的位置 2. 比对相互间的差值（注意首个位置为零）

```py
def max_str(string, seps):
    
    def kmp(t_str, p_str):
        """复习一遍KMP算法"""
        _p = []
        def get_next(p_str):
            _m = len(p_str)
            prefix, suffix = -1, 0
            _l = [-1] * _m

            while suffix < _m - 1:
                if prefix == -1 or p_str[suffix] == p_str[prefix]:
                    prefix, suffix = prefix + 1, suffix + 1
                    if _l[prefix] == _l[suffix]:
                        _l[suffix] = _l[prefix]
                    else:
                        _l[suffix] = prefix
                else:
                    prefix = _l[prefix - 1]

            return _l

        _get_next = get_next(p_str)

        m, n = len(p_str), len(t_str)
        i, j = 0, 0

        while j < n:
            if i == -1 or p_str[i] == t_str[j]:
                i, j = i + 1, j + 1
            else:
                i = _get_next[i]

            if i == m:
                _p.append(j - i)
                i = 0

        return _p
    # 获得分隔符的位置
    _ps = kmp(string, seps)
    max = 0
    _po = 0
    # 比较分隔符间隔大小，并获得其最大值的下标
    for i in range(len(_ps)):
        if i == 0:
            max = _ps[0]
            _po = 0
        elif _ps[i] - _ps[i - 1] > max:
            max = _ps[i] - _ps[i - 1]
            _po = i
    
    return string[_ps[_po - 1] + 1:_ps[_po]]
```



