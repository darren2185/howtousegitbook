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
> * str.count(sub[,start[,end]]) 计算sub在str中出现的次数，start表示开始位置，end表示结束位置, start和end可选
> * str.encode(encoding='utf-8', errors='strict') 返回加码的bytes字符串对象
> * str.endswith(suffix[,start[,end]]) 如果以suffix结尾为True，否则False
> * str.startswith(prefix[,start[,end]]) 如果以prefix结尾为True，否则False
> * str.find(sub[,start[,end]]) 查找sub，如有则True，反之False,类似'sub' in 'str'
> * str.format(\*arg, \*\*kwarg) 格式化字符串输出str.format(iterable),或者根据关键字{name}来填充。
> * str.format_map\(mapping\) 跟str.format()类似，仅能使用dict对象映射
> * str.index(sub[,start[,end]]) 跟find()类似，找sub的位置，若没有找到则ValueError
> * str.isalnum()  判断具体字符是不是跟字母跟数据
> * str.isalpha()  判断字符是不是为字母
> * str.isascii()  判断字母是否为ascii码
> * str.isdecimal() 判断是否为数字
> * str.isdigital() 





