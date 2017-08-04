# http协议   
### 介绍
 HTTP协议是Hyper Text Transfer Protocol（超文本传输协议）的缩写,
是用于从万维网（WWW:World Wide Web服务器传输超文本到本地浏览器的传送协议。

+ http（超文本传输协议）是一个基于请求与响应模式的、无状态的、应用层的协议 

> HTTP协议的主要特点可概括如下：  
  
  1.支持客户/服务器模式。
  2.简单快速：客户向服务器请求服务时，只需传送请求方法和路径。请求方法常用的有GET、HEAD、POST。每种方法规定了客户与服务器联系的类型不同。由于HTTP协议简单，使得HTTP服务器的程序规模小，因而通信速度很快。
  3.灵活：HTTP允许传输任意类型的数据对象。正在传输的类型由Content-Type加以标记。
  4.无连接：无连接的含义是限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接。采用这种方式可以节省传输时间。
  5.无状态：HTTP协议是无状态协议。无状态是指协议对于事务处理没有记忆能力。缺少状态意味着如果后续处理需要前面的信息，则它必须重传，这样可能导致每次连接传送的数据量增大。另一方面，在服务器不需要先前信息时它的应答就较快。  
### 一、URL
 HTTP使用统一资源标识符`(UniformResourceIdentifiers,URI)`来传输数据和建立连接。URL是一种特殊类型的URI，包含了用于查找某个资源的足够的信息
  URL,全称是UniformResourceLocator,中文叫统一资源定位符,是互联网上用来标识某一处资源的地址。以下面这个URL为例，介绍下普通URL的各部分组成：
  `http://www.aspxfans.com:8080/news/index.asp?boardID=5&ID=24618&page=1#name`
 格式如下：  
 http://host[":"port][abs_path]
 
>一个完整的URL包括以下几部分：

   1.协议部分：该URL的协议部分为“http：”，这代表网页使用的是HTTP协议。在Internet中可以使用多种协议，如HTTP，FTP等等本例中使用的是HTTP协议。在"HTTP"后面的“//”为分隔符
   
   2.域名部分：该URL的域名部分为`www.aspxfans.com`。一个URL中，也可以使用IP地址作为域名使用
   
   3.端口部分：跟在域名后面的是端口，域名和端口之间使用“:”作为分隔符。端口不是一个URL必须的部分，如果省略端口部分，将采用默认端口
   
   4.虚拟目录部分：从域名后的第一个“/”开始到最后一个“/”为止，是虚拟目录部分。虚拟目录也不是一个URL必须的部分。本例中的虚拟目录是“/news/”
   
   5.文件名部分：从域名后的最后一个“/”开始到“？”为止，是文件名部分，如果没有“?”,则是从域名后的最后一个“/”开始到“#”为止，是文件部分，如果没有“？”和“#”，那么从域名后的最后一个“/”开始到结束，都是文件名部分。本例中的文件名是“index.asp”。文件名部分也不是一个URL必须的部分，如果省略该部分，则使用默认的文件名
   
   6.锚部分：从“#”开始到最后，都是锚部分。本例中的锚部分是“name”。锚部分也不是一个URL必须的部分
   
   7.参数部分：从“？”开始到“#”为止之间的部分为参数部分，又称搜索部分、查询部分。本例中的参数部分为“boardID=5&ID=24618&page=1”。参数可以允许有多个参数，参数与参数之间用“&”作为分隔符。
> 补充(URI和URL的区别)

URI，是uniform resource identifier，统一资源标识符，用来唯一的标识一个资源。

>Web上可用的每种资源如HTML文档、图像、视频片段、程序等都是一个来URI来定位的
URI一般由三部组成：

1. 访问资源的命名机制
2. 存放资源的主机名
3. 资源自身的名称，由路径表示，着重强调于资源。

>URL是uniform-resource-locator,统一资源定位器，它是一种具体的URI，即URL可以用来标识一个资源，而且还指明了如何locate这个资源。

URL是Internet上用来描述信息资源的字符串，主要用在各种WWW客户程序和服务器程序上，特别是著名的Mosaic。
采用URL可以用一种统一的格式来描述各种信息资源，包括文件、服务器的地址和目录等。
>URL一般由三部组成：

1. 协议(或称为服务方式)
2. 存有该资源的主机IP地址(有时也包括端口号)
3. 主机资源的具体地址。如目录和文件名等

>URN，uniform-resource-name，统一资源命名，是通过名字来标识资源，比如mailto:java-net@java.sun.com。

>URI是以一种抽象的，高层次概念定义统一资源标识，而URL和URN则是具体的资源标识的方式。URL和URN都是一种URI。笼统地说，每个 URL 都是 URI，但不一定每个 URI 都是 URL。这是因为 URI 还包括一个子类，即统一资源名称 (URN)，它命名资源但不指定如何定位资源。上面的 mailto、news 和 isbn URI 都是 URN 的示例。

在Java的URI中，一个URI实例可以代表绝对的，也可以是相对的，只要它符合URI的语法规则。而URL类则不仅符合语义，还包含了定位该资源的信息，因此它不能是相对的。
在Java类库中，URI类不包含任何访问资源的方法，它唯一的作用就是解析。
相反的是，URL类可以打开一个到达资源的流。
### 二、请求  
>http请求由请求行（request-line）、请求头部（header）、空行和请求数据四个部分组成。

![http request](picture/HTTPRequest.png)

1. 请求行以方法符号开头，空格分开，然后是请求的URI和协议版本号  
> ######格式：Method Request-URI HTTP-Version CRLF
    其中Method表示请求方法；
    Request-URI是一个统一资源标识符；
    HTTP-Version表示请求的HTTP协议版本；
    CRLF表示回车和换行（除了作为结尾的CRLF外，不允许出现单独的CR或LF字符）。

> ###### GIT请求例子：  
    GET /562f25980001b1b106000338.jpg HTTP/1.1  
    Host    img.mukewang.com   
    User-Agent    Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.106 Safari/537.36   
    Accept    image/webp,image/*,*/*;q=0.8  
    Referer    http://www.imooc.com/   
    Accept-Encoding    gzip, deflate, sdch   
    Accept-Language    zh-CN,zh;q=0.8
>第一部分：请求行，用来说明请求类型,要访问的资源以及所使用的HTTP版本.

    GET说明请求类型为GET,[/562f25980001b1b106000338.jpg]为要访问的资源，
    该行的最后一部分说明使用的是HTTP1.1版本。

>第二部分：请求头部，紧接着请求行（即第一行）之后的部分，用来说明服务器要使用的附加信息

    从第二行起为请求头部，HOST将指出请求的目的地.User-Agent,
    服务器端和客户端脚本都能访问它,它是浏览器类型检测逻辑的重要基础.
    该信息由你的浏览器来定义,并且在每个请求中自动发送等等

>第三部分：空行，请求头部后面的空行是必须的

    即使第四部分的请求数据为空，也必须有空行。

>第四部分：请求数据也叫主体，可以添加任意的其他数据。

    这个例子的请求数据为空。
>######POST请求例子：

    POST / HTTP1.1
    Host:www.wrox.com
    User-Agent:Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 2.0.50727; .NET CLR 3.0.04506.648; .NET CLR 3.5.21022)
    Content-Type:application/x-www-form-urlencoded
    Content-Length:40
    Connection: Keep-Alive

    name=Professional%20Ajax&publisher=Wile
>第一部分：请求行，第一行明了是post请求，以及http1.1版本。

>第二部分：请求头部，第二行至第六行。

>第三部分：空行，第七行的空行。

>第四部分：请求数据，第八行。

> ######请求方法（所有方法全为大写）有多种，各个方法的解释如下：
    + GET     请求获取Request-URI所标识的资源
    + POST    在Request-URI所标识的资源后附加新的数据
    + HEAD    请求获取由Request-URI所标识的资源的响应消息报头
    + PUT     请求服务器存储一个资源，并用Request-URI作为其标识
    + DELETE  请求服务器删除Request-URI所标识的资源
    + TRACE   请求服务器回送收到的请求信息，主要用于测试或诊断
    + CONNECT 保留将来使用
    + OPTIONS 请求查询服务器的性能，或者查询与资源相关的选项和需求
  > 应用举例：
  + GET方法：在浏览器的地址栏中输入网址的方式访问网页时，
  浏览器采用GET方法向服务器获取资源，eg:GET /form.html HTTP/1.1 (CRLF)
  
  + POST方法要求被请求服务器接受附在请求后面的数据，常用于提交表单。
### 三、响应  
在接收和解释请求消息后，服务器返回一个HTTP响应消息。

>HTTP响应也由四个部分组成，分别是：状态行、消息报头、空行和响应正文。

![HTTP Response](picture/HTTPResponse.jpg)

> ######例子：
    HTTP/1.1 200 OK
    Date: Fri, 22 May 2009 06:07:21 GMT
    Content-Type: text/html; charset=UTF-8
    
    <html>
          <head></head>
          <body>
                <!--body goes here-->
          </body>
    </html>
>第一部分：状态行，由HTTP协议版本号， 状态码， 状态消息 三部分组成。
 
    第一行为状态行，（HTTP/1.1）表明HTTP版本为1.1版本，状态码为200，状态消息为（ok）

>1、状态行格式如下：

    HTTP-Version Status-Code Reason-Phrase CRLF
    HTTP-Version表示服务器HTTP协议的版本；
    Status-Code表示服务器发回的响应状态代码；
    Reason-Phrase表示状态代码的文本描述。

>第二部分：消息报头，用来说明客户端要使用的一些附加信息
 
>第二行和第三行为消息报头，

    Date:生成响应的日期和时间；Content-Type:指定了MIME类型的HTML(text/html),编码类型是UTF-8
 
>第三部分：空行，消息报头后面的空行是必须的
 
>第四部分：响应正文，服务器返回给客户端的文本信息。
 
    空行后面的html部分为响应正文。



>HTTP状态码
状态代码有三位数字组成，第一个数字定义了响应的类别，共分五种类别: 
      
        1xx：指示信息--表示请求已接收，继续处理
        2xx：成功--表示请求已被成功接收、理解、接受
        3xx：重定向--要完成请求必须进行更进一步的操作
        4xx：客户端错误--请求有语法错误或请求无法实现
        5xx：服务器端错误--服务器未能实现合法的请求
>常见状态代码、状态描述、说明：

    200 OK      //客户端请求成功
    400 Bad Request  //客户端请求有语法错误，不能被服务器所理解
    401 Unauthorized //请求未经授权，这个状态代码必须和WWW-Authenticate报头域一起使用 
    403 Forbidden  //服务器收到请求，但是拒绝提供服务
    404 Not Found  //请求资源不存在，eg：输入了错误的URL
    500 Internal Server Error //服务器发生不可预期的错误
    503 Server Unavailable  //服务器当前不能处理客户端的请求，一段时间后可能恢复正常
    eg：HTTP/1.1 200 OK （CRLF）

2、响应报头后述

3、响应正文就是服务器返回的资源的内容 
### 四、消息报头  
HTTP消息由客户端到服务器的请求和服务器到客户端的响应组成。请求消息和响应消息都是由开始行（对于请求消息，开始行就是请求行，对于响应消息，开始行就是状态行），消息报头（可选），空行（只有CRLF的行），消息正文（可选）组成。

>HTTP消息报头包括普通报头、请求报头、响应报头、实体报头。
每一个报头域都是由名字+“：”+空格+值 组成，消息报头域的名字是大小写无关的。

1、普通报头

>在普通报头中，有少数报头域用于所有的请求和响应消息，但并不用于被传输的实体，只用于传输的消息。eg：

>Cache-Control用于指定缓存指令，缓存指令是单向的（响应中出现的缓存指令在请求中未必会出现），且是独立的（一个消息的缓存指令不会影响另一个消息处理的缓存机制），HTTP1.0使用的类似的报头域为Pragma。
    
+ 请求时的缓存指令包括：no-cache（用于指示请求或响应消息不能缓存）、no-store、max-age、max-stale、min-fresh、only-if-cached;

+ 响应时的缓存指令包括：public、private、no-cache、no-store、no-transform、must-revalidate、proxy-revalidate、max-age、s-maxage.

+ eg：为了指示IE浏览器（客户端）不要缓存页面，服务器端的JSP程序可以编写如下：response.sehHeader("Cache-Control","no-cache");
    //response.setHeader("Pragma","no-cache");作用相当于上述代码，通常两者//合用
    这句代码将在发送的响应消息中设置普通报头域：Cache-Control:no-cache


>Date普通报头域表示消息产生的日期和时间

>Connection普通报头域允许发送指定连接的选项。例如指定连接是连续，或者指定“close”选项，通知服务器，在响应完成后，关闭连接

2、请求报头

>请求报头允许客户端向服务器端传递请求的附加信息以及客户端自身的信息。
常用的请求报头

    Accept
    Accept请求报头域用于指定客户端接受哪些类型的信息。eg：Accept：image/gif，表明客户端希望接受GIF图象格式的资源；Accept：text/html，表明客户端希望接受html文本。
    Accept-Charset
    Accept-Charset请求报头域用于指定客户端接受的字符集。eg：Accept-Charset:iso-8859-1,gb2312.如果在请求消息中没有设置这个域，缺省是任何字符集都可以接受。
    Accept-Encoding
    Accept-Encoding请求报头域类似于Accept，但是它是用于指定可接受的内容编码。eg：Accept-Encoding:gzip.deflate.如果请求消息中没有设置这个域服务器假定客户端对各种内容编码都可以接受。
    Accept-Language
    Accept-Language请求报头域类似于Accept，但是它是用于指定一种自然语言。eg：Accept-Language:zh-cn.如果请求消息中没有设置这个报头域，服务器假定客户端对各种语言都可以接受。
    Authorization
    Authorization请求报头域主要用于证明客户端有权查看某个资源。当浏览器访问一个页面时，如果收到服务器的响应代码为401（未授权），可以发送一个包含Authorization请求报头域的请求，要求服务器对其进行验证。
    Host（发送请求时，该报头域是必需的）
    Host请求报头域主要用于指定被请求资源的Internet主机和端口号，它通常从HTTP URL中提取出来的，eg：
    我们在浏览器中输入：http://www.guet.edu.cn/index.html
    浏览器发送的请求消息中，就会包含Host请求报头域，如下：
    Host：www.guet.edu.cn
    此处使用缺省端口号80，若指定了端口号，则变成：Host：www.guet.edu.cn:指定端口号
    User-Agent
>我们上网登陆论坛的时候，往往会看到一些欢迎信息，其中列出了你的操作系统的名称和版本，你所使用的浏览器的名称和版本，这往往让很多人感到很神奇，实际上，服务器应用程序就是从User-Agent这个请求报头域中获取到这些信息。User-Agent请求报头域允许客户端将它的操作系统、浏览器和其它属性告诉服务器。不过，这个报头域不是必需的，如果我们自己编写一个浏览器，不使用User-Agent请求报头域，那么服务器端就无法得知我们的信息了。
请求报头举例：

    GET /form.html HTTP/1.1 (CRLF)
    Accept:image/gif,image/x-xbitmap,image/jpeg,application/x-shockwave-flash,application/vnd.ms-excel,application/vnd.ms-powerpoint,application/msword,*/* (CRLF)
    Accept-Language:zh-cn (CRLF)
    Accept-Encoding:gzip,deflate (CRLF)
    If-Modified-Since:Wed,05 Jan 2007 11:21:25 GMT (CRLF)
    If-None-Match:W/"80b1a4c018f3c41:8317" (CRLF)
    User-Agent:Mozilla/4.0(compatible;MSIE6.0;Windows NT 5.0) (CRLF)
    Host:www.guet.edu.cn (CRLF)
    Connection:Keep-Alive (CRLF)
    (CRLF)

3、响应报头

> 响应报头允许服务器传递不能放在状态行中的附加响应信息，以及关于服务器的信息和对Request-URI所标识的资源进行下一步访问的信息。
常用的响应报头

    Location
    Location响应报头域用于重定向接受者到一个新的位置。Location响应报头域常用在更换域名的时候。
    Server
    Server响应报头域包含了服务器用来处理请求的软件信息。与User-Agent请求报头域是相对应的。下面是
    Server响应报头域的一个例子：
    Server：Apache-Coyote/1.1
    WWW-Authenticate
    WWW-Authenticate响应报头域必须被包含在401（未授权的）响应消息中，客户端收到401响应消息时候，并发送Authorization报头域请求服务器对其进行验证时，服务端响应报头就包含该报头域。
    eg：WWW-Authenticate:Basic realm="Basic Auth Test!"  //可以看出服务器对请求资源采用的是基本验证机制。


4、实体报头

>请求和响应消息都可以传送一个实体。一个实体由实体报头域和实体正文组成，但并不是说实体报头域和实体正文要在一起发送，可以只发送实体报头域。实体报头定义了关于实体正文（eg：有无实体正文）和请求所标识的资源的元信息。
常用的实体报头

    Content-Encoding
    Content-Encoding实体报头域被用作媒体类型的修饰符，它的值指示了已经被应用到实体正文的附加内容的编码，因而要获得Content-Type报头域中所引用的媒体类型，必须采用相应的解码机制。Content-Encoding这样用于记录文档的压缩方法，eg：Content-Encoding：gzip
    Content-Language
    Content-Language实体报头域描述了资源所用的自然语言。没有设置该域则认为实体内容将提供给所有的语言阅读者。eg：Content-Language:da
    Content-Length
    Content-Length实体报头域用于指明实体正文的长度，以字节方式存储的十进制数字来表示。
    Content-Type
    Content-Type实体报头域用语指明发送给接收者的实体正文的媒体类型。eg：
    Content-Type:text/html;charset=ISO-8859-1
    Content-Type:text/html;charset=GB2312
    Last-Modified
    Last-Modified实体报头域用于指示资源的最后修改日期和时间。
    Expires
    Expires实体报头域给出响应过期的日期和时间。为了让代理服务器或浏览器在一段时间以后更新缓存中(再次访问曾访问过的页面时，直接从缓存中加载，缩短响应时间和降低服务器负载)的页面，我们可以使用Expires实体报头域指定页面过期的时间。eg：Expires：Thu，15 Sep 2006 16:23:12 GMT
    HTTP1.1的客户端和缓存必须将其他非法的日期格式（包括0）看作已经过期。eg：为了让浏览器不要缓存页面，我们也可以利用Expires实体报头域，设置为0，jsp中程序如下：response.setDateHeader("Expires","0");
### 五、利用telnet观察http协议通讯过程   
实验目的及原理：
    利用MS的telnet工具，通过手动输入http请求信息的方式，向服务器发出请求，服务器接收、解释和接受请求后，会返回一个响应，该响应会在telnet窗口上显示出来，从而从感性上加深对http协议的通讯过程的认识。

> 实验步骤：  

>1、打开telnet

    1.1 打开telnet
    运行-->cmd-->telnet
    1.2 打开telnet回显功能
    set localecho
>2、连接服务器并发送请求

    2.1 open www.guet.edu.cn 80  //注意端口号不能省略

    HEAD /index.asp HTTP/1.0
    Host:www.guet.edu.cn
    /*我们可以变换请求方法,请求桂林电子主页内容,输入消息如下*/
    open www.guet.edu.cn 80 
   
    GET /index.asp HTTP/1.0  //请求资源的内容
    Host:www.guet.edu.cn  

    2.2 open www.sina.com.cn 80  //在命令提示符号下直接输入telnet www.sina.com.cn 80
    HEAD /index.asp HTTP/1.0
    Host:www.sina.com.cn
 

> 实验结果: 
  
>3.1 请求信息2.1得到的响应是:

    HTTP/1.1 200 OK                                              //请求成功
    Server: Microsoft-IIS/5.0                                    //web服务器
    Date: Thu,08 Mar 200707:17:51 GMT
    Connection: Keep-Alive                                 
    Content-Length: 23330
    Content-Type: text/html
    Expries: Thu,08 Mar 2007 07:16:51 GMT
    Set-Cookie: ASPSESSIONIDQAQBQQQB=BEJCDGKADEDJKLKKAJEOIMMH; path=/
    Cache-control: private

    //资源内容省略

>3.2 请求信息2.2得到的响应是:

    HTTP/1.0 404 Not Found       //请求失败
    Date: Thu, 08 Mar 2007 07:50:50 GMT
    Server: Apache/2.0.54 <Unix>
    Last-Modified: Thu, 30 Nov 2006 11:35:41 GMT
    ETag: "6277a-415-e7c76980"
    Accept-Ranges: bytes
    X-Powered-By: mod_xlayout_jh/0.0.1vhs.markII.remix
    Vary: Accept-Encoding
    Content-Type: text/html
    X-Cache: MISS from zjm152-78.sina.com.cn
    Via: 1.0 zjm152-78.sina.com.cn:80<squid/2.6.STABLES-20061207>
    X-Cache: MISS from th-143.sina.com.cn
    Connection: close


>失去了跟主机的连接

>按任意键继续...

>4 .注意事项：

    1、出现输入错误，则请求不会成功。  
    2、报头域不分大小写。  
    3、更深一步了解HTTP协议，可以查看RFC2616，在http://www.letf.org/rfc上找到该文件。  
    4、开发后台程序必须掌握http协议

### 六、HTTP工作原理  
>HTTP协议定义Web客户端如何从Web服务器请求Web页面，以及服务器如何把Web页面传送给客户端。
HTTP协议采用了请求/响应模型。客户端向服务器发送一个请求报文，请求报文包含请求的方法、URL、协议版本、请求头部和请求数据。
服务器以一个状态行作为响应，响应的内容包括协议的版本、成功或者错误代码、服务器信息、响应头部和响应数据。

>以下是 HTTP 请求/响应的步骤：

>1、客户端连接到Web服务器

    一个HTTP客户端，通常是浏览器，与Web服务器的HTTP端口（默认为80）
    建立一个TCP套接字连接。例如，http://www.oakcms.cn。

>2、发送HTTP请求

    通过TCP套接字，客户端向Web服务器发送一个文本的请求报文，
    一个请求报文由请求行、请求头部、空行和请求数据4部分组成。

>3、服务器接受请求并返回HTTP响应

    Web服务器解析请求，定位请求资源。服务器将资源复本写到TCP套接字，由客户端读取。
    一个响应由状态行、响应头部、空行和响应数据4部分组成。

>4、释放连接TCP连接

    若connection 模式为close，则服务器主动关闭TCP连接，
    客户端被动关闭连接，释放TCP连接;若connection 模式为keepalive，
    则该连接会保持一段时间，在该时间内可以继续接收请求;

>5、客户端浏览器解析HTML内容

    客户端浏览器首先解析状态行，查看表明请求是否成功的状态代码。
    然后解析每一个响应头，响应头告知以下为若干字节的HTML文档和文档的字符集。
    客户端浏览器读取响应数据HTML，根据HTML的语法对其进行格式化，并在浏览器窗口中显示。

>例如：在浏览器地址栏键入URL，按下回车之后会经历以下流程：

    1、浏览器向 DNS 服务器请求解析该 URL 中的域名所对应的 IP 地址;

    2、解析出 IP 地址后，根据该 IP 地址和默认端口 80，和服务器建立TCP连接;

    3、浏览器发出读取文件(URL 中域名后面部分对应的文件)的HTTP 请求，该请求报文作为 TCP 三次握手的第三个报文的数据发送给服务器;

    4、服务器对浏览器请求作出响应，并把对应的 html 文本发送给浏览器;

    5、释放 TCP连接;

    6、浏览器将该 html 文本并显示内容; 　　
### 七、HTTP协议相关技术补充

> 1、基础：  

>高层协议有：文件传输协议FTP、电子邮件传输协议SMTP、域名系统服务DNS、网络新闻传输协议NNTP和HTTP协议等
中介由三种：代理(Proxy)、网关(Gateway)和通道(Tunnel)，一个代理根据URI的绝对格式来接受请求，重写全部或部分消息，通过 URI的标识把已格式化过的请求发送到服务器。网关是一个接收代理，作为一些其它服务器的上层，并且如果必须的话，可以把请求翻译给下层的服务器协议。一 个通道作为不改变消息的两个连接之间的中继点。当通讯需要通过一个中介(例如：防火墙等)或者是中介不能识别消息的内容时，通道经常被使用。
     代理(Proxy)：一个中间程序，它可以充当一个服务器，也可以充当一个客户机，为其它客户机建立请求。请求是通过可能的翻译在内部或经过传递到其它的 服务器中。一个代理在发送请求信息之前，必须解释并且如果可能重写它。代理经常作为通过防火墙的客户机端的门户，代理还可以作为一个帮助应用来通过协议处 理没有被用户代理完成的请求。
网关(Gateway)：一个作为其它服务器中间媒介的服务器。与代理不同的是，网关接受请求就好象对被请求的资源来说它就是源服务器；发出请求的客户机并没有意识到它在同网关打交道。
网关经常作为通过防火墙的服务器端的门户，网关还可以作为一个协议翻译器以便存取那些存储在非HTTP系统中的资源。
    通道(Tunnel)：是作为两个连接中继的中介程序。一旦激活，通道便被认为不属于HTTP通讯，尽管通道可能是被一个HTTP请求初始化的。当被中继 的连接两端关闭时，通道便消失。当一个门户(Portal)必须存在或中介(Intermediary)不能解释中继的通讯时通道被经常使用。

>2、协议分析的优势—HTTP分析器检测网络攻击

>以模块化的方式对高层协议进行分析处理，将是未来入侵检测的方向。
HTTP及其代理的常用端口80、3128和8080在network部分用port标签进行了规定

>3、HTTP协议Content Lenth限制漏洞导致拒绝服务攻击

>使用POST方法时，可以设置ContentLenth来定义需要传送的数据长度，例如ContentLenth:999999999，在传送完成前，内 存不会释放，攻击者可以利用这个缺陷，连续向WEB服务器发送垃圾数据直至WEB服务器内存耗尽。这种攻击方法基本不会留下痕迹。
http://www.cnpaf.net/Class/HTTP/0532918532667330.html

>4、利用HTTP协议的特性进行拒绝服务攻击的一些构思

>服务器端忙于处理攻击者伪造的TCP连接请求而无暇理睬客户的正常请求（毕竟客户端的正常请求比率非常之小），此时从正常客户的角度看来，服务器失去响应，这种情况我们称作：服务器端受到了SYNFlood攻击（SYN洪水攻击）。
而Smurf、TearDrop等是利用ICMP报文来Flood和IP碎片攻击的。本文用“正常连接”的方法来产生拒绝服务攻击。
19端口在早期已经有人用来做Chargen攻击了，即Chargen_Denial_of_Service，但是！他们用的方法是在两台Chargen 服务器之间产生UDP连接，让服务器处理过多信息而DOWN掉，那么，干掉一台WEB服务器的条件就必须有2个：1.有Chargen服务2.有HTTP 服务
方法：攻击者伪造源IP给N台Chargen发送连接请求（Connect），Chargen接收到连接后就会返回每秒72字节的字符流（实际上根据网络实际情况，这个速度更快）给服务器。

>5、Http指纹识别技术  

>Http指纹识别的原理大致上也是相同的：记录不同服务器对Http协议执行中的微小差别进行识别.Http指纹识别比TCP/IP堆栈指纹识别复杂许 多,理由是定制Http服务器的配置文件、增加插件或组件使得更改Http的响应信息变的很容易,这样使得识别变的困难；然而定制TCP/IP堆栈的行为 需要对核心层进行修改,所以就容易识别.
      要让服务器返回不同的Banner信息的设置是很简单的,象Apache这样的开放源代码的Http服务器,用户可以在源代码里修改Banner信息,然 后重起Http服务就生效了；对于没有公开源代码的Http服务器比如微软的IIS或者是Netscape,可以在存放Banner信息的Dll文件中修 改,相关的文章有讨论的,这里不再赘述,当然这样的修改的效果还是不错的.另外一种模糊Banner信息的方法是使用插件。
常用测试请求：
1：HEAD/Http/1.0发送基本的Http请求
2：DELETE/Http/1.0发送那些不被允许的请求,比如Delete请求
3：GET/Http/3.0发送一个非法版本的Http协议请求
4：GET/JUNK/1.0发送一个不正确规格的Http协议请求
Http指纹识别工具Httprint,它通过运用统计学原理,组合模糊的逻辑学技术,能很有效的确定Http服务器的类型.它可以被用来收集和分析不同Http服务器产生的签名。

>6、其他：为了提高用户使用浏览器时的性能，现代浏览器还支持并发的访问方式，浏览一个网页时同时建立多个连接，以迅速获得一个网页上的多个图标，这样能更快速完成整个网页的传输。

>HTTP1.1中提供了这种持续连接的方式，而下一代HTTP协议：HTTP-NG更增加了有关会话控制、丰富的内容协商等方式的支持，来提供
更高效率的连接。
### 八、GET和POST请求的区别  
>GET请求

    GET /books/?sex=man&name=Professional HTTP/1.1
    Host: www.wrox.com
    User-Agent: Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.7.6)
    Gecko/20050225 Firefox/1.0.1
    Connection: Keep-Alive
    注意最后一行是空行

>POST请求

    POST / HTTP/1.1
    Host: www.wrox.com
    User-Agent: Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.7.6)
    Gecko/20050225 Firefox/1.0.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 40
    Connection: Keep-Alive  
    //空行
    name=Professional%20Ajax&publisher=Wiley
>1、GET提交，请求的数据会附在URL之后（就是把数据放置在HTTP协议头中），
以?分割URL和传输数据，多个参数用&连接；

    例 如：login.action?name=hyddd&password=idontknow&verify=%E4%BD%A0 %E5%A5%BD。
    如果数据是英文字母/数字，原样发送，如果是空格，转换为+，如果是中文/其他字符，
    则直接把字符串用BASE64加密，得出如： %E4%BD%A0%E5%A5%BD，
    其中％XX中的XX为该符号以16进制表示的ASCII。

>POST提交：把提交的数据放置在是HTTP包的包体中。
>上文示例中红色字体标明的就是实际的传输数据

因此，GET提交的数据会在地址栏中显示出来，而POST提交，地址栏不会改变

>2、传输数据的大小：首先声明：HTTP协议没有对传输的数据大小进行限制，HTTP协议规范也没有对URL长度进行限制。
而在实际开发中存在的限制主要有：

    GET:特定浏览器和服务器对URL长度有限制，例如 IE对URL长度的限制是2083字节(2K+35)。对于其他浏览器，如Netscape、FireFox等，理论上没有长度限制，其限制取决于操作系 统的支持。

    因此对于GET提交时，传输数据就会受到URL长度的 限制。

    POST:由于不是通过URL传值，理论上数据不受 限。但实际各个WEB服务器会规定对post提交数据大小进行限制，Apache、IIS6都有各自的配置。

>3、安全性

    POST的安全性要比GET的安全性高。比如：通过GET提交数据，用户名和密码将明文出现在URL上，因为(1)登录页面有可能被浏览器缓存；(2)其他人查看浏览器的历史纪录，那么别人就可以拿到你的账号和密码了，除此之外，使用GET提交数据还可能会造成Cross-site request forgery攻击

>4、Http get,post,soap协议都是在http上运行的

    （1）get：请求参数是作为一个key/value对的序列（查询字符串）附加到URL上的
    查询字符串的长度受到web浏览器和web服务器的限制（如IE最多支持2048个字符），不适合传输大型数据集同时，它很不安全

    （2）post：请求参数是在http标题的一个不同部分（名为entity body）传输的，这一部分用来传输表单信息，因此必须将Content-type设置为:application/x-www-form- urlencoded。post设计用来支持web窗体上的用户字段，其参数也是作为key/value对传输。
    但是：它不支持复杂数据类型，因为post没有定义传输数据结构的语义和规则。

    （3）soap：是http post的一个专用版本，遵循一种特殊的xml消息格式
    Content-type设置为: text/xml 任何数据都可以xml化。

    Http协议定义了很多与服务器交互的方法，最基本的有4种，分别是GET,POST,PUT,DELETE. 一个URL地址用于描述一个网络上的资源，而HTTP中的GET, POST, PUT, DELETE就对应着对这个资源的查，改，增，删4个操作。 我们最常见的就是GET和POST了。GET一般用于获取/查询资源信息，而POST一般用于更新资源信息.

>我们看看GET和POST的区别

    GET提交的数据会放在URL之后，以?分割URL和传输数据，参数之间以&相连，如EditPosts.aspx?name=test1&id=123456. POST方法是把提交的数据放在HTTP包的Body中.

    GET提交的数据大小有限制（因为浏览器对URL的长度有限制），而POST方法提交的数据没有限制.

    GET方式需要使用Request.QueryString来取得变量的值，而POST方式通过Request.Form来获取变量的值。

    GET方式提交数据，会带来安全问题，比如一个登录页面，通过GET方式提交数据时，用户名和密码将出现在URL上，如果页面可以被缓存或者其他人可以访问这台机器，就可以从历史记录获得该用户的账号和密码.





















































