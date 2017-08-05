#PDO对数据库的操作  

>链接到数据库  

    <?php
    /**
     * Created by PhpStorm.
     * User: zhong
     * Date: 2017/8/4
     * Time: 2:40
     */
    header("Content-type:text/html;charset=utf8");
    $servername = 'localhost';
    $username='root';
    $password='';
    try{
        $connect = new PDO('mysql:host='.$servername.';charset=utf8',$username,$password);
        //设置PDO错误模式为异常
        $connect->setAttribute(PDO::ATTR_ERRMODE,PDO::ERRMODE_EXCEPTION);
        
        echo 'OK<br>';
    }catch (PDOException $e){
        echo "<br>" . $e->getMessage();
    }
    $connect = null;
    
>注意：在链接的时候指定字符集utf8

>创建数据库  

    <?php
    /**
     * Created by PhpStorm.
     * User: zhong
     * Date: 2017/8/5
     * Time: 14:44
     */
    $servername='localhost';
    $username='root';
    $password='';
    $dbname='userdb';
    try{
        $con = new PDO("mysql:host=".$servername,$username,$password);
        //SQL语句拼接的时候一定要有空格
        $sql="CREATE DATABASE ".$dbname;
        $con->exec($sql);
        echo "ok";
    }catch (PDOException $e){
        echo $e->getMessage();
    }
>注意点：SQL语句在拼接时，一定要和拼接变量之间有个空格，不然会报错

>知识点：CREATE DATABASE databasename(创建数据库)

>创建表   

    <?php
    /**
     * Created by PhpStorm.
     * User: zhong
     * Date: 2017/8/5
     * Time: 14:11
     */
    $servername='localhost';
    $username='root';
    $password='';
    $dbname='myBDPDO';
    
    try{
        $con = new PDO("mysql:host=".$servername.";dbname=".$dbname.";charset=utf8",$username,$password);
        $con->setAttribute(PDO::ATTR_ERRMODE,PDO::ERRMODE_EXCEPTION);
        //UNSIGNED丢了N导致报错
        //创建表的sql语句
        $sql="CREATE TABLE MyGuests(
        id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY  KEY ,
        firstname NVARCHAR(30) NOT NULL,
        lastname NVARCHAR(30) NOT NULL,
        email NVARCHAR(50),
        reg_data TIMESTAMP
    )";
        $con->exec($sql);
    }catch (PDOException $e){
        echo $e->getMessage();
    }
>注意点：创建表时，字符串的类型定义为Nchar或Nvarchar，不然当存入中文或一些其它字符时，在数据库中显示为？

>知识点：
> char是定长的，也就是当你输入的字符小于你指定的数目时，char(8)，你输入的字符小于8时，
它会再后面补空值。当你输入的字符大于指定的数时，它会截取超出的字符。

> nvarchar(n)包含n个字符的可变长度 Unicode 字符数据。n 的值必须介于 1 与 4,000 之间。
字节的存储大小是所输入字符个数的两倍。所输入的数据字符长度可以为零。 
      
>varchar[(n)] 长度为 n 个字节的可变长度且非 Unicode 的字符数据。
n 必须是一个介于 1 和 8,000 之间的数值。存储大小为输入数据的字节的实际长度，
而不是 n 个字节。所输入的数据字符长度可以为零。

+ CHAR。CHAR存储定长数据很方便，CHAR字段上的索引效率级高，比如定义char(10)，那么不论你存储的数据是否达到了10个字节，都要占去10个字节的空间。     
+ VARCHAR。存储变长数据，但存储效率没有CHAR高。如果一个字段可能的值是不固定长度的，我们只知道它不可能超过10个字符，把它定义为 VARCHAR(10)是最合算的。VARCHAR类型的实际长度是它的值的实际长度+1。为什么“+1”呢？这一个字节用于保存实际使用了多大的长度。从空间上考虑，用varchar合适；从效率上考虑，用char合适，关键是根据实际情况找到权衡点。  
+ TEXT。text存储可变长度的非Unicode数据，最大长度为2^31-1(2,147,483,647)个字符。  
* NCHAR、NVARCHAR、NTEXT。这三种从名字上看比前面三种多了个“N”。它表示存储的是Unicode数据类型的字符。我们知道字符中，英文字符只需要一个字节存储就足够了，但汉字众多，需要两个字节存储，英文与汉字同时存在时容易造成混乱，Unicode字符集就是为了解决字符集这种不兼容的问题而产生的，它所有的字符都用两个字节表示，即英文字符也是用两个字节表示。nchar、nvarchar的长度是在1到4000之间。和char、varchar比较起来，nchar、nvarchar则最多存储4000个字符，不论是英文还是汉字；而char、varchar最多能存储8000个英文，4000个汉字。可以看出使用nchar、nvarchar数据类型时不用担心输入的字符是英文还是汉字，较为方便，但在存储英文时数量上有些损失。所以一般来说，如果含有中文字符，用nchar/nvarchar，如果纯英文和数字，用char/varchar。  

>在表中插入数据  

    <?php
    /**
     * Created by PhpStorm.
     * User: zhong
     * Date: 2017/8/4
     * Time: 2:40
     */
    header("Content-type:text/html;charset=utf8");
    $servername = 'localhost';
    $username='root';
    $password='';
    $dbname='myBDPDO';
    $myuser= array(
        array('李','小红','123@12306.com'),
        array('赵','xiaolan','321com')
    );
    try{
        //最好设置要设置charset=utf8;不然当向表中添加中文数据时，可能会报错
        $connect = new PDO('mysql:host='.$servername.';dbname='.$dbname.';charset=utf8',$username,$password);
        //设置PDO错误模式为异常
        $connect->setAttribute(PDO::ATTR_ERRMODE,PDO::ERRMODE_EXCEPTION);
        //开始事务
        $connect->beginTransaction();
        //向表中插入数据
        for($i=0;$i<count($myuser);$i++){
        $sql = "INSERT INTO MyGuests(firstname,lastname,email) 
            VALUES ('".$myuser[$i][0]."','".$myuser[$i][1]."','".$myuser[$i][2]."')";
    
        //使用exec()，没有返回结果
        $connect->exec($sql);
        }
        //提交事务
        $connect->commit();
        echo 'OK<br>';
    
    }catch (PDOException $e){
        //失败回滚
        $connect->rollBack();
        echo "<br>" . $e->getMessage();
    }
    $connect = null;  
>知识点：
+ 数组操作：求取数组的长度count();
+ SQL语句 INSERT INTO tablename VALUES();
>注意点：  
- 链接的时候要设置字符集为utf8  

>删除表  
    
    <?php
    /**
     * Created by PhpStorm.
     * User: zhong
     * Date: 2017/8/5
     * Time: 13:48
     */
    $servername="localhost";
    $username="root";
    $password="";
    $dbname = "myBDPDO";
    try{
        $conn=new PDO("mysql:host=".$servername.";dbname=".$dbname.";charset=utf8",$username,$password);
    
        $conn->setAttribute(PDO::ATTR_ERRMODE,PDO::ERRMODE_EXCEPTION);
    
        $sql = "DROP TABLE myGuests";
        $conn->exec($sql);
    }catch (PDOException $e){
        echo $e->getMessage();
    }
    
> 删除数据库  

    <?php
    /**
     * Created by PhpStorm.
     * User: zhong
     * Date: 2017/8/5
     * Time: 15:01
     */
    $servername='localhost';
    $username='root';
    $password='';
    $databaseName='userdb';
    try{
        $con = new PDO("mysql:host=".$servername,$username,$password);
        $con->setAttribute(PDO::ATTR_ERRMODE,PDO::ERRMODE_EXCEPTION);
        //拼接的前方有个空格，不然会报错
        $sql="DROP DATABASE ".$databaseName;
        $con->exec($sql);
        echo 'OK';
    }catch (PDOException $e){
        echo $e->getMessage();
    }
>获取数据库信息   

    <?php
    /**
     * Created by PhpStorm.
     * User: zhong
     * Date: 2017/8/5
     * Time: 15:40
     */
    $servername='localhost';
    $username='root';
    $password="";
    $dbname = "myBDPDO";
    $tablename = 'myGuests';
    try{
        $con = new PDO("mysql:host=".$servername.";dbname=".$dbname.";charset=utf8",$username,$password);
        $con->setAttribute(PDO::ATTR_ERRMODE,PDO::ERRMODE_EXCEPTION);
        $sql="SELECT * FROM ".$tablename." WHERE firstname='赵'";
        $result=$con->query($sql);
        while ($row=$result->fetch()) {
            echo "firstname: ".$row["firstname"]."<br>";
            echo "lastname: ".$row["lastname"]."<br>";
            echo "email: ".$row["email"]."<br>";
        }
    }catch (PDOException $e){
        echo $e->getMessage();
    }
>知识点：    
+ PDO::query执行一条SQL语句，如果通过，则返回一个PDOStatement对象。PDO::query函数有个“非常好处”，就是可以直接遍历这个返回的记录集。
示例如下：
$sql = 'SELECT name FROM url';
foreach ($dbh->query($sql) as $row) {
    print $row['name'] . "\t";
}
query同传统的MySQL query函数类似，同样需要对开发者自行对输入的sql语句进行安全检查。
query因为会返回PDOStament对象，似乎用在SELECT语句执行上更合适，这跟上文提到的query支持直接遍历不谋而合。
query执行后，在下一次query执行之前，如果不取走所有返回的记录集，则query将会执行失败，除非我们调用 PDOStatement::closeCursor()来释放数据库资源与PDOStatement对象。  
+ PDO::exec
  PDO::exec执行一条SQL语句，并返回受影响的行数。此函数不会返回结果集合。官方建议：
  对于在程序中只需要发出一次的 SELECT 语句，可以考虑使用 PDO::query()。
  对于需要发出多次的语句，可用 PDO::prepare() 来准备一个 PDOStatement 对象并用 PDOStatement::execute() 发出语句。
  PDO::exec支持SELECT/DELETE/UPDATE/INSERT等全部SQL语句执行，所以相比PDO query()函数功能要强大的多。由于只返回受影响的函数，所以，如果执行SELECT则无法得到PDOStatement对象，故也无法遍历结果集，只能按照官方建议去使用query或execute函数。