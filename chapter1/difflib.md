# difflib - Helpers for Computing Deltas

此模块提供对比序列的类和方法，能用于如对比文件，生成各种文件格式的差异信息清单，如HMTL，上下文和统一差异，为了比对文件夹或者文件，请参照filecmp模块

##### class difflib.SequenceMatcher

这是一个对比任何类型的弹性类，数据类型需能可hashable，

##### class difflib.Differ

此类用于对于对比行文本，并且能生成可读性差异信息， Differ使用SequenceMatcher去对比行文本序列，也能对比相似行字符序列，对比后信息显示：

| Code | Meaning |
| :---: | :---: |
| '- ’ | line unique to sequence 1 |
| '+ ' | line unique to sequence 2 |
| '  ' | line common to both sequences |
| '? ' | line not present in either inputsequence |

行以？开始，需试图集中眼神区分差异，且都不在两者之间显示，类似于这样行含有tab字符的，容易造成混淆

##### class difflib.HtmlDiff

可用于创建HTML表，将显示以行对比行，左右对照，此表能生成全部或者上下文差异模式

\__\_init\_\(tabsize=8, wrapcolumn=None, linejunk=None, charjunk=ISCHARACTER\_JUNK\)\_实例化HtmlDiff， tabsize为可选项，默认8个空字符

wrapcolumen为可选项，描述一行字符为多少后自动换行，默认值为None，指不自动换行

linejunk和charjunk均为可选项，传递给ndiff\(\)函数，用于生成左右差异对比信息，关于ndiff\(\)，请见下

> * _make\_file\(fromlines, tolines, fromdesc='', todesc='', context=False, numlines=5, \*, charset='utf-8'\) _对比fromlines和tolines将返回一个字符串,\(HTML文件含差异对比信息\)，fromdesc和todesc为可选参数，描述from/to文件表头字符，context和numlines为可选参数，设context为真时，则前后对比差异将会显示，默认值为FALSE，显示所有文件
> * make_table\(fromlines, tolines, fromdesc='', todesc='',context=False, numlines=5\) 与make\_file类似，将生成包含差异化信息的HTML表格_
> * difflib.context\_diff\(a, b, fromfile='', tofile='', fromfiledate='', tofiledate='', n=3, lineterm='\n'\) 对比a和b，返回上下文格式的差异信息，



