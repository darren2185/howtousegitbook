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



