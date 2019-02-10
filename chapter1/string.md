# string: Common string operations

### class str

class str\(object=''\)  
class str\(object=b'', encoding='utf-8', errors='strict'\)  
将返回一个string对象，如果object为空，则返回空字符，否则依据encoding和errors：

> 若encoding和errors为空，str\(object\)则会根据object.\_\_str\_\_\(\)返回字符串，或者返回repr\(object\)  
> 若encoding和errors非空, object则要求为bytes-like对象（二进制对象，bytes和bytearray）, str\(bytes, encoding, errors\)相当于bytes.decode\(encoding, errors\)

#### String Methods

> * str.capitalize\(\) 首字符大写
> * str.casefold\(\) 转特殊字符成小写形式：German lowercase letter 'ß' is equivalent to "ss". Since it is already lowercase, lower\(\) would do nothing to 'ß'; casefold\(\) converts it to "ss".
> * str.center\(width\[,fillchar\]\)在width宽度中居中，fillchar表示空白填充字符
> * str.ljust\(width\[,fillchar\]\) 字符串的宽度大于字符串长度时，左对齐，其右侧则为padding,或者由其他字符替代
> * str.rjust\(width\[,fillchar\]\) 字符串的宽度大于字符串长度时，右对齐，其左侧则为padding,或者由其他字符替代
>   ```py
>   #如果用len(str)来测试字符长度均为20，其涵盖了替代字符的长度
>   str.center(20,' ') #第二个参数必须为实质性的字符，空白或者其他
>   str.ljust(20, '*')
>   str.rjust(20)
>   ```
> * str.count\(sub\[,start\[,end\]\]\) 计算sub在str中出现的次数，start表示开始位置，end表示结束位置, start和end可选
> * str.encode\(encoding='utf-8', errors='strict'\) 返回加码的bytes字符串对象
> * str.endswith\(suffix\[,start\[,end\]\]\) 如果以suffix结尾为True，否则False
> * str.startswith\(prefix\[,start\[,end\]\]\) 如果以prefix结尾为True，否则False
> * str.format\(\*arg, \*\*kwarg\) 格式化字符串输出str.format\(iterable\),或者根据关键字{name}来填充。
> * str.format\_map\(mapping\) 跟str.format\(\)类似，仅能使用dict对象映射
> * str.index\(sub\[,start\[,end\]\]\) 跟find\(\)类似，找sub的位置，若没有找到则ValueError
> * str.rindex\(sub\[,start\[,end\]\]\) 类似rfind\(\),若没有找到结果，则引起ValueError
> * str.find\(sub\[,start\[,end\]\]\) 查找sub，如有则True，反之False,类似'sub' in 'str'
> * str.rfind\(sub\[,start\[,end\]\]\) 从右侧开始寻找sub子字符串，start和end表示起始与终止区间，如果寻找到则返回index位置，否则返回-1\(False\)
>
> * str.isalnum\(\) 判断具体字符是不是跟字母跟数据
>
> * str.isalpha\(\) 判断字符是不是为字母
> * str.isascii\(\) 判断字母是否为ascii码
> * str.isdecimal\(\) 判断是否为数字
> * str.isdigital\(\) 如果所有字符为数字或者至少一个字符为数字，则为True，否则为False,Numeric\_Type= Digit或者Numeric\_Type=Numeric
> * str.isprintable\(\) 判断字符是否可打印或显示
> * str.isspace\(\) 判断该字符是否为空格符
> * str.istitle\(\) 判断是否字符串中每个单词是否首字母大写\(即标题字符\)
> * str.isupper\(\) 若所有字符均为大写字符，则为True,否则为False
> * str.join\(iterable\) 将可迭代性的对象连接成一个字符串，如果iterable中含有non-string对象则会引起TypeError，iterable中不同元素间可以自定义separator分隔符，由str决定，例如
>   ```py
>   ','.join(['d','c','e','f']) #'d,c,e,f'
>   '/'.join(['d','c','e','f']) #'d/c/e/f'
>   ```
> * str.lower\(\) 返回字符串全转换为小写的副本
> * str.upper\(\) 返回字符串全转换为大写的副本
> * str.strip\(\) 返回去掉首尾字符的副本，chars参数为描述要删除字符的集合，如忽略或者None，则默认删除空白字符，chars并不是指前缀或者后缀
> * str.lstrip\(\[chars\]\) 返回去掉首字符的字符串副本，chars参数为描述要删除字符的集合，如忽略或者None，则默认删除空白字符，chars不是个字符前缀，则其所有可能组合字符串的均会被删除
> * str.rstrip\(\[chars\]\) 返回去掉尾部字符的字符串副本，关于chars见上
>   ```py
>   ' spacious '.strip() # spacious
>   'www.example.com'.strip('cmowz.') # example
>   comment_string='#......Section 3.2.1 Issue #32....#'
>   comment_string.strip('#.') #Section 3.2.1 Issue #32'
>   ' spacious '.lstrip() #'spacious '
>   'www.example.com'.lstrip('cmowz.') #'example.com'
>   ' spacious '.rstrip() #' spacious'
>   'mississippi'.rstrip('ipz') #'mississ'
>   ```
> * str.partition\(sep\) 分割按sep为基础的字符串，并返回包含三个元素的tuple，第一个为第一次遇到分隔符前部部分，第二个为分隔符本身，第三个为分隔符之后部分。如果分隔符没在字符中，则第一个为字符串本身，余下均为空字符串
> * str.rpartition\(sep\) 分割以sep的字符串，并返回包含三个元素的tuple，第一个为右侧开始第一个分隔符之前的所有字符，第二个为分隔符本身，第三个为分割符之后
> * str.replace\(old,new\[,count\]\) 用子串new替换子串old，并返回替换字符串后的字符串副本，count参数则明示替换的参数,如果count大于old出现的次数，则表示替换所有old字符串
> * str.rsplit\(sep=None, maxsplit=-1\) 返回以sep作为分隔符的字符串单词列表，如果maxsplit被赋予，则就会执行maxsplit次，其余在不会再执行，当maxsplit为默认值-1或者没有描述时，根据sep出现次数来分割字符串;当sep没有描述或者None，任何空白字符均为分隔符。
> * str.split\(sep=None, maxsplit=1\) 返回以sep作为分割符的字符串单词列表，如果maxsplit被赋予，则就会执行maxsplit次，其余在不会再执行，当maxsplit为默认值-1或者没有描述时，根据sep出现次数来分割字符串;
> * str.split\(\[chars\]\) 返回一个首尾均去掉了
>   ```py
>   '1,2,3'.split(',') #['1','2','3']
>   '1,2,3,4'.split(',',maxsplit=2) #['1','2','3,4']
>   '1,2,,3'.split(',') #['1','2','','3']
>   ```
> * str.splitlines\(\[keepends\]\) 返回以行结束符为边界的列表，行结束符不包含在列表元素中，除非参数keepends给出或者为True

| Representation | Description |
| :--- | :--- |
| \n | Line Feed |
| \r | Carriage Return |
| \r\n | Carriage Return + Line Feed |
| \v or \x0b | Line Tabulation |
| \f Or \x0c | Form Feed |
| \x1c | File Separator |
| \x1d | Group Separator |
| \x1e | Record Separator |
| \x85 | Next Line\(C1 Control Code\) |
| \u2028 | Line Separator |
| \u2029 | Paragraph Separator |

```py
'ab c\n\nde fg\rkl\r\n'.splitlines() #['ab c','','de fg','kl']
'ab c\n\nde fg\rkl\r\n'.splitlines(keepends=True) #['ab c\n','\n','de fg\r','kl\r\n']
```

> 和split\(\)不同，当sep指定，split\(\)将返回一个空列表，以下示例作为对比：
>
> ```py
> "".splitlines() # []
> "One line\n".splitlines() #[’One line']
> "".split('\n') #['']
> "Two lines\n'.split('\n') #['Two lines']
> ```
>
> * str.title\(\)返回一个单词首字母均为大写的字符串
>   ```py
>   'Hello world'.title() # 'Hello World'
>   "they're bill's friends from the UK".title()
>   # 'They'Re Bill'S Friends From The Uk'
>   import re
>   def titlecase(s):
>     return re.sub(r'[A-Za-z]+('[A-Za-z]+)?',lambda mo:mo.group(0)[0].upper() + mo.group(0)[1:].lower(),s)
>   titlecase("they're bill's friends.") # They're Bill's Friends
>   ```
> * str.zfill\(width\) 返回左侧填充了ASCII '0'使其长度为width的字符串副本



