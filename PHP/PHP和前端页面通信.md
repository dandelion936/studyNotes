# PHP文件和前端页面数据交互

> 前端向PHP发送数据  
    代码示例：
      
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <title>Title</title>
            <script src="jquery-3.2.1.js"></script>
            <style>
                div a{
                    color: red;
                }
            </style>
        </head>
        <body>
            <div>淘宝</div>
            <div>京东</div>
        </body>
        <script>
            $('div').click(function () {
                var $_this = $(this);
                var $_this_text = $(this).html();
                console.log({name:$_this_text});
                $.ajax({
                    type:'POST',
                    url:'post.php',
                    contentType:'application/json;charset=utf-8',
                    data:{name:$_this_text},
                    success:function (data) {
                        console.log(data);
                        $_this.html(data);
                    }
        
                })
        
            })
        </script>
        </html>
>使用Ajax向PHP页面发送数据

>后端获取前端发送的数据，然后响应前端的请求  
    代码示例：
    
        <?php
        /**
         * Created by PhpStorm.
         * User: zhong
         * Date: 2017/8/4
         * Time: 2:40
         */
        /*function myTest(){
            $a=["hello","php",3];
            for($i=0;$i<count($a);$i++){
                echo "<p>".$a[$i]."</p>";
            }
        }
        myTest();*/
        header("Content-Type:text/html;charset=utf-8");
        $username=explode("=",file_get_contents('php://input'));
        //前端通过Ajax发送的数据，PHP通过file_get_contents('php://input')获取，不能通过$_POST获取
        
        //print_r(urldecode($username[1]));
        //urldecode()解码：还原 URL 编码字符串。
        class Site{
            var $url;
            var $title;
            function setUrl($par)
            {
                $this->url = $par;
            }
            function setTitle($title){
                $this->title=$title;
            }
            function  getUrl(){
                echo "<a href='".$this->url . PHP_EOL."'>".$this->title . PHP_EOL."</a>";
            }
        
        }
        $taobao = new Site;
        $taobao->setUrl('https://www.taobao.com/');
        $taobao->setTitle('淘宝');
        
        $jd = new Site;
        $jd->setUrl('https://www.jd.com/');
        $jd->setTitle('京东');
        switch (urldecode($username[1])){
            case '淘宝':
                $taobao->getUrl();
                break;
            case '京东':
                $jd->getUrl();
                break;
        }

>file_get_contents("php://input")和$_POST/GIT的区别  

+ php://input 允许读取 POST 的原始数据。
和 $HTTP_RAW_POST_DATA 比起来，它给内存带来的压力较小，并且不需要任何特殊的 php.ini 设置。
php://input 不能用于 enctype="multipart/form-data"。

+ $_POST 变量是一个数组,内容是由 HTTP POST 方法发送的变量名称和值.
  $_POST 变量用于收集来自 method="post" 的表单中的值,从带有 POST 方法的表单发送的信息,
  对任何人都是不可见的(不会显示在浏览器的地址栏),并且对发送信息的量也没有限制.
  
> 字符串操作之explode()函数   
1. 定义和用法
   
  > explode() 函数把字符串打散为数组。
   注释："separator" 参数不能是一个空字符串。
   注释：该函数是二进制安全的。
   相关函数：implode()用自定义连接符把数组组成字符串  
   
2.语法
  
     explode(separator,string,limit)   
3. 参数	描述
   
   >separator	必需。规定在哪里分割字符串。  
   string	必需。要分割的字符串。   
   limit	可选。规定所返回的数组元素的数目。  
   可能的值：  
   大于 0 - 返回包含最多 limit 个元素的数组  
   小于 0 - 返回包含除了最后的 -limit 个元素以外的所有元素的数组   
   0 - 返回包含一个元素的数组
   
> urlencode()编码：对字符串中除了 -_. 之外的所有非字母数字字符都将被替换成百分号（%）后跟两位十六进制数，空格则编码为加号（+）。
  urldecode()解码：还原 URL 编码字符串。
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
