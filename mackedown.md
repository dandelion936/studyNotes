一、标题  
=== 
*1. 类setex形式*    

最高阶标题  
===

第二阶标题
---
*2.类Atx形式*  
# h1 # 
## h2 ##  
### h3 ###  
# 二、引用 #   
*   断行引用
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
> 
> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
> id sem consectetuer libero luctus adipiscing.
* 整段引用
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.Donec sit amet nisl.   

> Aliquam semper ipsum sit amet velit. Suspendisse
id sem consectetuer libero luctus adipiscing.  
* 引用嵌套  
> This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.
+ 引用区块可以包含标题、列表、代码区块  
> ## 这是一个标题。
> 
> 1.   这是第一行列表项。
> 2.   这是第二行列表项。
> 
> 给出一些例子代码：
>
>     return shell_exec("echo $input | $markdown_script");  
三、列表
===
1. 无序列表  
三种无序列表的生成方式星号、加号、减号  
> *   Red
> *   Green
> *   Blue  

> +   Red
> +   Green
> +   Blue  

> -   Red
> -   Green
> -   Blue  
2. 有序列表  
可以不按照顺序也可按照顺序
3. 说明  
+ 列表项目中有空行分开解析成HTML时将会用p标签包裹
+ 列表中可以包含多个段落，必须用4空格或1制表符缩进  
+ 列表项目内放引用，>必须缩进  
+ 如果放代码块，区块缩进两次（8空格或2制表符） 
+ 行首出现数字-句点-空白，要避免这样的状况，你可以在句点前面加上反斜杠。  
# 四代码区块 
1. 代码区块很简单，只要简单地缩进4个空格或是1个制表符就可以,每一行的空格或制表符在解析的时候会被移除    
Here is an example of AppleScript:

    tell application "Foo"
        beep
    end tell
2. HTML的源码加上缩进就行了  
    <div class="footer">
        &copy; 2004 Foo Corporation
    </div>
# 五分割线  
一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格。  
# 六区段元素 
1. 行内式   
+ 插入网址链接
> This is [an example](http://example.com/ "Title") inline link.  
> [This link](http://example.net/) has no title attribute.  
+ 链接同主机资源  
> See my [About](/about/) page for details.
3.  参考式  
> This is [an example][id] reference-style link.  

> [id]: http://example.com/  "Optional Title Here"
+ 链接内容定义的形式为：
  
  > 方括号（前面可以选择性地加上至多三个空格来缩进），里面输入链接文字
  接着一个冒号
  接着一个以上的空格或制表符
  接着链接的网址
  选择性地接着 title 内容，可以用单引号、双引号或是括弧包着   
 * 相同的链接定义  
 [foo]: http://example.com/  "Optional Title Here"  
 [foo]: http://example.com/  'Optional Title Here'  
  [foo]: http://example.com/  (Optional Title Here)  
  + 链接不区分大小写  
  > [link text][a]  
  > [link text][A]  
  
  - 隐式链接标记功能让你可以省略指定链接标记，这种情形下，链接标记会视为等同于链接文字，要用隐式链接标记只要在链接文字后面加上一个空的方括号  
    [Google]: http://google.com/  
# 七强调  
1. 星号（*）  
> *single asterisks*  

2. 底线（_）  
> _single underscores_  

3. 如果你的 * 和 _ 两边都有空白的话，它们就只会被当成普通的符号。  
> _ single underscores _  
# 八代码  
1. 小段行内代码用(`)包裹起来  
> Use the `printf()` function.  

2. 如果要在代码区段内插入反引号，你可以用多个反引号来开启和结束代码区段：  
> ``There is a literal backtick (`) here.``
3. 代码区段内，& 和方括号都会被自动地转成 HTML 实体
> Please don't use any `<blink>` tags.
# 九图片  
1. 行内式  
 ![Alt text](/path/to/img.jpg)
 
 ![Alt text](/path/to/img.jpg "Optional title")  
 详细叙述如下：
 
 - 一个惊叹号 !
 - 接着一个方括号，里面放上图片的替代文字
 - 接着一个普通括号，里面放上图片的网址，最后还可以用引号包住并加上 选择性的 'title' 文字 
2. 参考式  
 ![Alt text][id]  
 「id」是图片参考的名称，图片参考的定义方式则和连结参考一样  
 [id]: url/to/image  "Optional title attribute"  
# 十其他
1. 自动链接  
<http://example.com/>  
2. 反斜杠  
> \   反斜线
  `   反引号
  \*   星号
  _   底线
  {}  花括号
  []  方括号
  ()  括弧
  \#   井字号
  \+   加号
  \-   减号
  .   英文句点
  !   惊叹号