# MarkdownTutor

## 标题语法
要创建标题，请在单词或短语前面添加井号 (#) 。# 的数量代表了标题的级别。
```
# Heading level 1
```

## 段落语法
要创建段落，请使用空白行将一行或多行文本进行分隔。
```
I really like using
Markdown.
```

## 换行语法
在一行的末尾添加两个或多个空格，然后按回车键,即可创建一个换行`<br>`。
为了兼容性，请在行尾添加“结尾空格”或 HTML 的 `<br> `标签来实现换行。
```
First line with the HTML tag after.<br>
And the next line.
```

## 强调语法
通过将文本设置为粗体或斜体来强调其重要性。

- 粗体 要加粗文本，请在单词或短语的前后各添加两个星号（asterisks）或下划线（underscores）。如需加粗一个单词或短语的中间部分用以表示强调的话，请在要加粗部分的两侧各添加两个星号（asterisks）。
```
I just love **bold text**.
```

- 斜体 要用斜体显示文本，请在单词或短语前后添加一个星号（asterisk）或下划线（underscore）。要斜体突出单词的中间部分，请在字母前后各添加一个星号，中间不要带空格。
```
Italicized text is the *cat's meow*.
```

- 粗体和斜体 要同时用粗体和斜体突出显示文本，请在单词或短语的前后各添加三个星号或下划线。要加粗并用斜体显示单词或短语的中间部分，请在要突出显示的部分前后各添加三个星号，中间不要带空格。
```
This is really***very***important text.
```

## 引用语法 
要创建块引用，请在段落前添加一个 > 符号。
```
> Dorothy followed her through many of the beautiful rooms in her castle.
```

## 列表语法 
可以将多个条目组织成有序或无序列表。

- 有序列表 要创建有序列表，请在每个列表项前添加数字并紧跟一个英文句点。数字不必按数学顺序排列，但是列表应当以数字 1 起始。
```
1. First item
2. Second item
```

- 无序列表 要创建无序列表，请在每个列表项前面添加破折号 (-)、星号 (*) 或加号 (+) 。缩进一个或多个列表项可创建嵌套列表。 
```
- First item
- Second item
- Third item
- Fourth item
```

## 代码语法 
- 要将单词或短语表示为代码，请将其包裹在反引号 (`) 中。
```
At the command prompt, type `nano`.
```
- 转义反引号
如果你要表示为代码的单词或短语中包含一个或多个反引号，则可以通过将单词或短语包裹在双反引号(``)中。
```
``Use `code` in your Markdown file.``
```
- 代码块
Markdown基本语法允许您通过将行缩进四个空格或一个制表符来创建代码块。如果发现不方便，请尝试使用受保护的代码块。根据Markdown处理器或编辑器的不同，您将在代码块之前和之后的行上使用三个反引号（```）或三个波浪号（~~~）。
```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

## 分割线语法
要创建分隔线，请在单独一行上使用三个或多个星号 (***)、破折号 (---) 或下划线 (___) ，并且不能包含其他内容。
```
Try to put a blank line before...

---

...and after a horizontal rule.
```

## 链接语法
链接文本放在中括号内，链接地址放在后面的括号中，链接title可选。
```
[超链接显示名](超链接地址 "超链接title")
```

## 图片语法
要添加图像，请使用感叹号 (!), 然后在方括号增加替代文本，图片链接放在圆括号里，括号里的链接后可以增加一个可选的图片标题文本。
```
![图片alt](图片链接 "图片title")
```

## 转义字符语法
要显示原本用于格式化 Markdown 文档的字符，请在字符前面添加反斜杠字符 \ 。
``` 
\* Without the backslash, this would be a bullet in an unordered list.
```
渲染效果如下：<br>
\* Without the backslash, this would be a bullet in an unordered list.
