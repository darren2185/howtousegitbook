## 字符串

---

基于字符串处理的需要，要求字符集上有一种确定的序关系，称为字符序，字符串可以看做一类特殊的线性表，表中元素取自选定的字符集。

* 字符串的长度
* 字符在字符串的位置
* 字符串相等\(=、&gt;、&lt;、in、is\)
* 字典序
* 字符串拼接 \(+\)
* 子串关系\(index, find,replace\)
* 前缀与后缀\(startswith, endwith\)
* 其他有用的串运算 s \* n

字符串集合和拼接操作构成了一种代数结构，空串是拼接操作的”单位元“：s1 + \(s2 + s3\)=\(s1 + s2\) + s3

字符串ADT

```
ADT String:
    String(self, sseq)        #基于字符序列sseq建立一个字符串
    is_empty(self)            #判断本字符串是否为空
    len(self)                 #取得字符串的长度
    char(self, index)         #取得字符串中位置index的字符
    substr(self, a, b)        #取得字符串中[a:b]的子串，左闭右开区间
    match(self, string)       #查找字符串string在本字符串中第一个出现的位置
    concat(self, string)      #做出本字符串与另一字符串string的拼接串
    subset(self, str1, str2)  #做出将本字符串里的子串str1都替换为str2的结果串
```

1. 字符串内容的存储。1，把一个字符串的全部内容存储在一块连续存储区里；2，把串中的每个字符单独存入一个独立存储块，并将这些块链接起来。连续存储的主要问题是需要大块存储，极长的字符串可能带来问题；而一个字符一块存储，需要附加一个链接域，额外存储开销比较大。实际中完全可以采用某种中间方式，把一个串的字符序列分段保存在一块存储块里，并链接起来这些存储块。
2. 串结束的表示。不同字符串的长度可能不同，由于存储在计算机里的都是二进制编码，从存储内容无法判断哪里是串的结束。1，用一个专门的数据域记录字符串长度，2，用一个特殊编码表示串结束，为此需要保证该编码不代表任何字符。

#### 串匹配算法

如果从目标串的某个位置i开始，模式串里的每个字符串都与目标串里的对应字符相同，就是找到了一个匹配。如果在比较中遇到了一对不同的字符，那就是不匹配，说明模式串不能与目标串中从位置i开始的子串匹配。串匹配算法设计的关键有两点：

1. 怎样选择开始比较的字符对
2. 发现了不匹配后，下一步怎么做。

朴素的串匹配算法采用最直观可行的策略：1，从左到右逐个字符串匹配；2，发现不匹配时，转去考虑目标串里的下一个位置是否与模式串匹配。

1. 主串S的第一位开始，S与T得前三个字母都匹配成功，但S得第四个字母是d而T的是g。第一位匹配失败。如图所示，竖直连线表示相等，弯折线表示不等。  
   ![](/assets/4.1.png)

2. 主串S第二位开始，主串S首字母为o，模式串T的首字母为g，匹配失败，如图所示：

   ![](/assets/4.2.png)

   3.主串S第三位开始，主串S首字母为o，模式串T的首字母为g，匹配失败，如图所示：

   ![](/assets/4.3.png)

   4.主串S第四位开始，主串S首字母为d，模式串T的首字母为g，匹配失败，如图所示：

   ![](/assets/4.4.png)

   5.主串S第五位开始，S与T，6个字母全匹配，匹配成功，如图所示：

   ![](/assets/4.5.png)

```py
def naive_matching(t, p):
   """朴素模式匹配算法"""
   """t为目标串，p为模式串"""
    m, n = len(p), len(t)
    i, j = 0, 0

    while i < m and j < n:
        if p[i] == t[j]:
            # 如果p[i]与t[j],两者都往后移动一位
            i, j = i + 1, j + 1
        else:
            # 否则i回到模式串的起始位置，j则往下移动一位，继续匹配
            i, j = 0, j - i + 1

        if i == m:
            # 当模式串所有都匹配时，则返回模式串在目标串的下标位置
            yield j - i
            i = 0
    return
```

#### KMP算法

KMP算法的基本想法是匹配中不回溯。如果匹配中用模式串里的pi匹配某个tj时失败了（遇到了pj ≠ tj的情况），就找到了某个特定的Ki\(0 ≤ Ki &lt; i \)，下一步用模式串中的字符Pki与目标字符串里的Tj比较，在匹配失败时把模式串前移若干位置，用模式串里匹配失败字符之前的某个字符与目标串中匹配失败的字符比较。

文本串S匹配到 i 位置，模式串P匹配到 j 位置

* 如果j = -1，或者当前字符匹配成功（即S\[i\] == P\[j\]），都令i++，j++，继续匹配下一个字符；
* 如果j != -1，且当前字符匹配失败（即S\[i\] != P\[j\]），则令 i 不变，j = next\[j\]。此举意味着失配时，模式串P相对于文本串S向右移动了j - next \[j\] 位。

换言之，当匹配失败时，模式串向右移动的位数为：失配字符所在位置 - 失配字符对应的next 值（next 数组的求解会在下文的**移动的实际位数为：j - next\[j\]**，且此值大于等于1。

```py
def kmp(s, p):

    def get_next(pat_str):
        """获取偏移数组"""
        _n = len(pat_str)
        prefix = -1     # 前缀指针， -1是标记符，当为-1时，则目标字符串后移一位
        suffix = 0      # 后缀指针
        _l = [-1] * _n  # 初始化数组
        while suffix < _n - 1:
            # 当prefix为-1，或者prefix与suffix相等时后移一位。
            if prefix == -1 or pat_str[prefix] == pat_str[suffix]:   
                prefix, suffix = prefix + 1, suffix + 1

                # 如何实现快速跳转
                # 当某个字符前后相等时，当模式字符串与目标字符不等时，则其前字符也不相等，直接跳到其前位置（字符不相等位置处）
                if pat_str[suffix] == pat_str[prefix]:               
                    _l[suffix] = _l[prefix]
                else:
                    _l[suffix] = prefix
            else:
                prefix = _l[prefix]

        return _l
    # 获取偏移数组  
    _next_list = get_next(p)
    # print(_next_list)
    # 获取模式字符串及目标字符串长度
    n, m = len(s), len(p)
    i, j = 0, 0

    while i < n and j < m:
        # 向后偏移的条件两个：1. j为-1,2. 目标字符串[i]与模式字符串[j]相等时
        if j == -1 or s[i] == p[j]:
            i, j = i + 1, j + 1
        else:
            # 如果不满足，则从偏移数组中获取偏移模式串位置量    
            j = _next_list[j]
        if j == m:
            # 迭代生成器
            yield i - j
            # 当某处已完全匹配后，跳转下一位置继续匹配。
            j = 0
```

#### Boyer Moore算法

#### AC算法



