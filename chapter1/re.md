# Regular Expression

---

re模块提供正则表达式来匹配操作类似于Perl，模式字符与字符均可使用Unicode和8位字符，当然两者不能混合，原因不能通过byte类型数据来匹配Unicode编码数据，正如替代字符操作时，被替代的数据与替代数据的类型需一致才行。正则表达式使用下划线“\”来指示特殊形式或者允许特殊字符才不会唤起其特殊意义表达。

## **正则表达式语法**

正则表达式就是描述一组字符匹配它，而函数则让你检查是否一组字符能匹配特定的正则式。

| .\(Dot\) | 默认值，能匹配任何字符除了换行符，如果DOTALL为TRUE,则会匹配所有字符含换行符 |
| :--- | :--- |
| ^\(Caret\) | 匹配开始字符，在MULTILINE模式也会匹配每行 |
| $ | 匹配结尾字符,'foo'能匹配‘foo’和‘foobar’,如果使用**foo$**则只能匹配‘foo’ |
| \* | 匹配0或者多个字符，ab\*将匹配‘a’，‘ab’或者‘ab...b’任意个b的字符串 |
| + | 匹配至少1个或者多个字符，ab+将匹配‘ab’或‘ab...b’任意多个b的字符串 |
| ? | 匹配0个或者1个字符串，ab?将匹配‘a’和‘ab’ |
| \*?,+?,?? | \*,+,?均为贪婪字符，它们尽可能多的匹配字符，有时不希望出现这样的结果，如\&lt;.\_\&gt;匹配' b ' ,将返回整串字符，而不是希望的\，如果在后面加上？则为非贪婪模式或者最小匹配，故&lt;.\_?&gt;才能匹配 |
| {m} | 精准描述匹配m次数才会匹配成功，少了不会匹配成功，例如，a{6}将匹配a出现6次的字符串，而不是5次 |
| {m,n} | 匹配从m次到n次出现的字符，视图尽可能多的匹配，例如，a{3,5}将匹配3到5个a的字符，忽略m将从下界0开始，而忽略n则到无限，例如，a{4,}将匹配’aaaab’或者一千个‘a’b的字符，逗号不能忽略，否则与{m}类似 |
| {m,n}? | 匹配从m次到n次出现的字符，非贪婪模式，尽可能少的匹配。例如，a{3,5}b将匹配aaaaaab后5位a，如果使用a{3,5}?b则尽可能少的匹配，aaab此模式需要待求证，目前在python模块中，re测试的结果还是贪婪模式 |
| \\(backslash\) | 当需要匹配正则表达式特殊字符时，如\*，?，\[，\]，{，}等需要使用backslash \指示需要匹配特殊字符 |
| \[\] | 用作指示字符集合1.字符列表，\[amk\]将会匹配‘a’,’m’,’k’2.指示两个字符范围，如\[a-z\]表示a到z的所有小写字母，\[0-5\]表示从0至5之间的数字，而\[0-9a-zA-Z\]匹配所有字母及数字，\[a-z\]仅匹配a,-,z三个字符3.括号中特殊字符将失去其本身意义作为单纯字符而匹配，\[\(+\*\)\]则匹配‘\(’,’+’,’\*’,’\)’4.字符类如\s或\S在括号中能被接受5.如果括号中首字符为^，则括号中所有字符将不会匹配，如\[^5\]将匹配除了5的所有字符，\[^^\]将匹配除了^的所有字符6.如果需要匹配‘\]’则需要借助backslash \\] |
| \| | A\|B，表示RE将从左至右来匹配A或者B，如A匹配则B将会忽略，如果需要匹配‘\|’可以借助\\|和\[\|\] |
| \(…\) | 正则表达式匹配分组，括号中内容将会匹配后被检索 |
| \(?P&lt;name&gt;.. \) | 分组 |
| \(?aiLmsux | 字母分别代表：re.A\(仅匹配ASCII\)，re.I\(忽略大小写\)，re.L\(本地化\)，re.M\(多行\)，re.S\(.匹配所有字符\)，re.U\(匹配Unicode\)，re.X\(冗长\) |
| \(?:…\) |  |
| \(?aiLmsux-imsx:…\) |  |
| \(?\#...\) | 正则表达式注释 |
| \(?=…\) | 当…匹配时，才会匹配其前面字符串，因此叫做lookahead assertion，例如Isaac \(?=Asimov\)将会匹配‘Isaac’，仅当其后跟有’Asimov’ |
| \(?!...\) | 与上述相反，例如Isaac \(?!Asimov\)能匹配Isaac Darren，但不会匹配Isaac Asimov |
| \(?&lt;=…\) | \(?&lt;=abc\)def将会匹配’abcdef’，只能用来匹配固定长度的字符，而a\*诸如此类则不行 |
| \(?&lt;!...\) | 与上述相反 |
| \(?\(id/name\)yes-pattern\|no-pattern\) |  |
| \A |  |
| \b | 匹配空字符，但仅在单词的开头和结尾处，r’\bfoo\b’ foo,foo.,\(foo\),bar foo baz |
| \B | 与上述相反，r‘py\B’能匹配python,py3,py2,不能匹配py,py.,py! |
| \d | 匹配数字【0-9】 |
| \D | 非数字 |
| \s | 匹配空白字符 |
| \S | 匹配非空白字符 |
| \w | 匹配字符【0-9a-zA-Z】 |
| \W | 匹配非字符【0-9a-zA-Z】 |

## Module Contents

模块中定义了几个函数、常量和一个异常

> * re.compile\(pattern,flags=0\)编译pattern并生成regular expression object，其能应用到match\(\)，search\(\)及其他方法中，而表达式的行为能受flags的值改变而调整执行流程如下：
>
>   ```py
>   Prog = re.compile\(pattern\)
>   Result = prog.match\(string\)
>   # 与以下相当
>   result = re.match\(pattern,string\)
>   ```
>
>   但如果预先编译了正则表达式，则后续应用能加快匹配速度
>
> * re.A or re.ASCII 使\w，\W，\b，\B，\d，\D，\s和\S只能匹配ASCII
>
> * re.U or re.UNICODE 则与ASCII码相对而言
>
> * re.DEBUG 显示调试信息
>
> * re.I or re.IGNORECASE  用作忽略大小写
>
> * re.L or re.LOCALE 使\w，\W，\b，\B匹配取决于本地化，主要用bytes pattern
>
> * re.M or re.MULTILINE 多行模式
>
> * re.S or re.DOTALL 使.能匹配任意字符
>
> * re.X or re.VERBOSE 主要为了编码pattern的排版清晰
>
> * ```py
>   a = re.compile(r"""\d+ # the integral part
>                      \.  # the decimal point
>                      \d* # some fractional digitals""", re.X)
>   b = re.compile(r'\d+\.\d*')
>   ```
> * re.search\(pattern, string, flags=0\)  扫描整串字符找到第一个为匹配模式字符的字符串，然后返回match object，若返回None则意味着字符没有匹配结果
>
> * re.match\(pattern, string, flags=0\)  如果0或者多个字符在开始位置匹配正则式，将返回match object，否则返回None，此方法仅匹配开始位置，若寻找其他位置则使用re.search\(\)
>
> * re.fullmatch\(pattern, string, flags = 0\) 如果整串字符都匹配则返回match object,否则返回None
>
> * re.split\(pattern, string, maxsplit=0, flags=0\) 根据正则表达式分割字符串
>
> * re.findall\(pattern, string, flags=0\)   从左到右扫描，然后返回所有符合正则式的字符列表
>
> * re.finditer\(pattern, string, flags=0\)  返回一个迭代器，其作用与re.findall\(\)类似
>
> * re.sub\(pattern, repl, string, count=0, flags=0\) 字符替代
>
> * re.subn\(pattern, repl, string, count = 0, flags=0\)
>
> * re.escape\(pattern\)
>
> * re.error\(msg, pattern=None, pos=None\)

### Regular Expression Objects

经编译后的REO对象支持以下方法和属性

> * Pattern.search\(string\[,pos\[,endpos\]\]\) 扫描字符串寻找第一处满足正则式，并返回match object，返回None则没有找到满足正则式的字符串，注意和寻找0长度不同，pos表示开始位置，endpos表示结束位置。rx.search\(string, 0, 50\) == rx.search\(string\[:50\],0\)
>
> ```py
> pattern = re.compile(r'd')
> pattern.search('dog')    # <re.Match object; span=(0,1), match='d'>
> type(pattern.search('dog',1)) # NoneType
> ```
>
> * Pattern.match\(string\[,pos\[,endpos\]\]\) 如果从0或更多字符在字符开头开始匹配此正则表达式，则返回match object,如果不匹配则返回None，pos表示开始位置，endpos表示结束位置
>
> ```py
> pattern = re.compile("o")
> pattern.match("dog")   # No match as "o" is not at the start of "dog".
> pattern.match("dog",1) # Match as "o" is the 2nd character of "dog" 
> <re.Match object; span=(1,2),match='o'>
> #如果要定位字符中任何位置时，请使用search()
> ```
>
> * Pattern.split\(string, maxsplit=0\)  与re.split\(\)相同，区别在于需要先编译正则式
> * Pattern.findall\(string\[,pos\[,endpos\]\]\) 和re.findall\(\)相同
> * Pattern.finditer\(string\[,pos\[,endpos\]\]\) 和re.finditer\(\)相同
> * Pattern.sub\(repl, string,count=0\)
> * Pattern.subn\(repl,string,count=0\)
> * Pattern.flags
> * Pattern.groups  在模式中的组数量
> * Pattern.groupindex 组中位置
> * Pattern.pattern  返回正则式

### Match Objects

Match object只有True值，否则为None,如match\(\)或者search\(\)方法返回值，match object支持以下方法：

> * Match.expand\(template\) 该方法利用一个类似sub方法，将template中用反斜杠标示的数字或者组名替代为相应的组中值
>
> ```py
> m = re.match(r'(?P<first_name>\w+) (?P<last_name>\w+)','Eric Brown')
> print(m.groups()) 'Eric' 'Brown'
> print(m.expand(r'His name is \1 \2)) # His name is Eric Brown
> print(m.expand(r'His name is \g<1> \g<2>')) # His name is Eric Brown
> print(m.expand(r'His name is \g<first_name> \g<last_name>')) # His name is Eric Brown
> ```
>
> * Match.group\(\[group1,...\]\) 如果参数为单个数值则返回相应坐标的值，如果参数为多个值，则返回tuple列表，当然所赋予参数均要满足小于或者等于最大groups数
>
> ```py
> m = re.match(r'(\w+) (\w+)',"Isaac Newton, physicist")
> m.group(0)   #'Isaac Newton'
> m.group(1)   #'Isaac’
> m.group(2)   #'Newton"
> m.group(1,2) #('Isaac', 'Newton')
>
> m = re.match(r"(?P<fist_name>\w+) (?P<last_name>\w+)',"Malcolm Reynolds")
> m.group('first_name') #Malcolm
> m.group('last_name')  # Reynolds
>
> m = re.match(r'(..)+','a1b2c3')
> m.group(1) #c3
> ```
>
> * Match.\_\_getitem\_\_\(g\) 和m.group\(g\)类似，方便访问每个group
>
> ```py
> m[0],m[1]
> ```
>
> m.groups\(default=None\) 返回tuple列表，包含所有组
>
> ```py
> m = re.match(r'(\d+)\.(\d+)','24.1632') 
> m.gropus() #('24','1632')
> ```
>
> * Match.groupdict\(default=None\) 返回一个字典
>
> ```py
> m = re.match(r"(?P<first_name>\w+) (?P<last_name>\w+)","Malcolm Reynolds")
> m.groupdict() #{'first_name':'Malcolm','last_name':'Reynolds'}
> ```
>
> * Match.start\(\[group\]\)
> * Match.end\(\[group\]\) 返回正则表达式中的组匹配的子字符串在原字符串中的起始与结束位置，默认值为0示例：
>
>   ```
>   email="tony@tiremove_thisget.net"
>   m = re.search("remove_this",email)
>   email[:m.start()] +email[m.end():] #tony@tiger.net
>   ```
>
> * Match.span\(\[group\]\) 返回一组（开始位置，结束位置）值
>
> * Match.pos  Match.endpos 匹配字符开始位置跟结束位置
>
> * Match.lastindex
>
> * Match.lastgroup
>
> * Match.re
>
> * Match.string

#### Regular Expression Examples

```py
def displaymatch(match):
    if match is None:
        return None
    return '<Match: %r, groups=%r>'%(match.group(), match.groups())

valid = re.compile(r"^[a2-9tjqk]{5}$")
displaymatch(valid.match("akt5q"))  #Valid  "<Match:'akt5q', groups=()>"
displaymatch(valid.match('akt5e'))  #Invalid
displaymatch(valid.match('akt'))    #Invalid
displaymatch(valid.match("727ak"))  #Valid  "<Match:'727ak', groups=()>"')

pair = re.compile(r".*(.).*\1")  #匹配重复字符
displaymatch(pair.match('717ak'))  # '<Match: '717', groups=('7',)>'
displaymatch(pair.match('718ak'))  # none
displaymatch(pair.match('354aa'))  # '<Match: 'aa', groups=('a',)>'

```



