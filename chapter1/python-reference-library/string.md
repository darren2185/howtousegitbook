# string: Common string operations

### class str

class str\(object=''\)  
class str\(object=b'', encoding='utf-8', errors='strict'\)  
将返回一个string对象，如果object为空，则返回空字符，否则依据encoding和errors：

> 若encoding和errors为空，str\(object\)则会根据object.\_\_str\_\_\(\)返回字符串，或者返回repr\(object\)   
> 若encoding和errors非空, object则要求为bytes-like对象（二进制对象，bytes和bytearray）, str\(bytes, encoding, errors\)相当于bytes.decode\(encoding, errors\)

#### String Methods

> * str.capitalize\(\)  首字符大写
> * str.casefold\(\)    转特殊字符成小写形式：German lowercase letter 'ß' is equivalent to "ss". Since it is already lowercase, lower() would do nothing to 'ß'; casefold() converts it to "ss".
> * str.center(width[,fillchar])在width宽度中居中，fillchar表示空白填充字符
> * str.ljust(width[,fillchar]) 字符串的宽度大于字符串长度时，左对齐，其右侧则为padding,或者由其他字符替代
> * str.rjust(width[,fillchar]) 字符串的宽度大于字符串长度时，右对齐，其左侧则为padding,或者由其他字符替代
```py
#如果用len(str)来测试字符长度均为20，其涵盖了替代字符的长度
str.center(20,' ')  #第二个参数必须为实质性的字符，空白或者其他
str.ljust(20, '*')
str.rjust(20)
```
> * str.count(sub[,start[,end]]) 计算sub在str中出现的次数，start表示开始位置，end表示结束位置, start和end可选
> * str.encode(encoding='utf-8', errors='strict') 返回加码的bytes字符串对象
> * str.endswith(suffix[,start[,end]]) 如果以suffix结尾为True，否则False
> * str.startswith(prefix[,start[,end]]) 如果以prefix结尾为True，否则False
> * str.format(\*arg, \*\*kwarg) 格式化字符串输出str.format(iterable),或者根据关键字{name}来填充。
> * str.format_map\(mapping\) 跟str.format()类似，仅能使用dict对象映射
> * str.index(sub[,start[,end]]) 跟find()类似，找sub的位置，若没有找到则ValueError
> * str.rindex(sub[,start[,end]]) 类似rfind(),若没有找到结果，则引起ValueError
> * str.find(sub[,start[,end]]) 查找sub，如有则True，反之False,类似'sub' in 'str'
> * str.rfind(sub[,start[,end]]) 从右侧开始寻找sub子字符串，start和end表示起始与终止区间，如果寻找到则返回index位置，否则返回-1(False)

> * str.isalnum()  判断具体字符是不是跟字母跟数据
> * str.isalpha()  判断字符是不是为字母
> * str.isascii()  判断字母是否为ascii码
> * str.isdecimal() 判断是否为数字
> * str.isdigital() 如果所有字符为数字或者至少一个字符为数字，则为True，否则为False,Numeric\_Type= Digit或者Numeric\_Type=Numeric
> * str.isprintable() 判断字符是否可打印或显示
> * str.isspace() 判断该字符是否为空格符
> * str.istitle() 判断是否字符串中每个单词是否首字母大写(即标题字符)
> * str.isupper() 若所有字符均为大写字符，则为True,否则为False
> * str.join(iterable) 将可迭代性的对象连接成一个字符串，如果iterable中含有non\-string对象则会引起TypeError，iterable中不同元素间可以自定义separator分隔符，由str决定，例如
```py
','.join(['d','c','e','f'])   #'d,c,e,f'
'/'.join(['d','c','e','f'])   #'d/c/e/f'
```
> * str.lower() 返回字符串全转换为小写的副本
> * str.lstrip([chars]) 返回去掉首字符的字符串副本，chars参数为描述要删除字符的集合，如忽略或者None，则默认删除空白字符，chars不是个字符前缀，则其所有可能组合字符串的均会被删除
> * str.rstrip([chars]) 返回去掉尾部字符的字符串副本，关于chars见上
```py
'    spacious   '.lstrip() #'spacious   '
'www.example.com'.lstrip('cmowz.') #'example.com'
``` 
> * str.partition(sep) 分割按sep为基础的字符串，并返回包含三个元素的tuple，第一个为第一次遇到分隔符前部部分，第二个为分隔符本身，第三个为分隔符之后部分。如果分隔符没在字符中，则第一个为字符串本身，余下均为空字符串
> * str.rpartition(sep) 分割以sep的字符串，并返回包含三个元素的tuple，第一个为右侧开始第一个分隔符之前的所有字符，第二个为分隔符本身，第三个为分割符之后
> * str.replace(old,new[,count]) 用子串new替换子串old，并返回替换字符串后的字符串副本，count参数则明示替换的参数,如果count大于old出现的次数，则表示替换所有old字符串
> * 



