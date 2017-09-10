# Mysql

正确地创建并合理地使用索引是一种技术能力。


## 索引理解

索引类型:

    主键
    唯一键
    非主码索引
    全文索引
    空间类型


## 问题解答

一个表只能有一个主键,一个表只能有一个聚集索引?

    因为主键的作用就是把表的数据格式转换成索引(平衡树)的格式存放。

无主键的表与有主键的表的区别?

    无主键的表的数据无序地存放在磁盘上,有主键的表的数据树状地存放在磁盘上。

索引的有副作用吗?

    首先索引是有序存储,并且以搜索为目的进行了优化。索引就像书的目录,自然能提高查询
    的速度,但是每给字段新建一个索引,字段中的数据就会被复制一份,用于生成索引,占用
    的磁盘空间就会增大。并且平衡树是一种平衡状态,任何的增删改都会导致平衡树的重建,
    而平衡树的重建需要一定的开销。


## 常用操作

基本命令：

    explain: 查看运行当前sql语句的QEP
    explain partitions: 查看特定表分区的附加信息
    explain extensions: 深入理解实际执行的sql语句
    show create table: 呈现当前表的列和索引定义细节
    show indexes: 查看索引信息
    show table status: 查看数据库表的底层大小及表结构(引擎类型、版本、数据、索引及行的平均长度)
    show status: 用来查看当前msyql服务器的当前内部状态信息
    show variables: 查看mysql系统变量的当前值

安装授权：

    yum安装：
        yum install mysql-server
    修改权限：
        chown -R root:root /var/lib/mysql
    重启mysql：
        service mysqld restart
    修改密码：
        > UPDATE user SET Password=password('新密码') WHERE User='root';
    重启mysql服务：
        service mysqld restart
    连接授权：
        > update user set host='%' where user='root';    //这个命令执行错误时可略过
        > flush privileges;
        > select host, user from user; //检查‘%’ 是否插入到数据库中
        > quit;


## 系统变量

全局内存缓冲区:

    key_buffer_size:  myisam索引码的缓冲区的大小,通常也成为码缓存
    innodb_buffer_pool_size: 定义innodb缓冲池大小
    innodb_additional_mem_pool_size: 定义innodb数据字典以及内部数据缓冲区的大小
    query_cache_size: 定义查询缓存的大小,查询缓存可以用来缓存经常执行的select语句

全局/会话内存缓冲区

    max_heap_table_size: 定义memory存储引擎表的最大容量
    tmp_table_size: 定义了一个内部基于内存的临时表的最大容量

会话缓冲区

    join_buffer_size: 定义了当索引无法满足条件时在两个表之间做全表连接操作能够使用的内存缓冲区大小
    sort_buffer_size: 定义了当索引无法满足需要的顺序信息是对结果排序能够使用的内存缓冲区的大小
    read_buffer_size: 定义了连续数据扫描时能够使用的内存缓冲区大小
    read_rnd_buffer_size: 定义了有序数据扫描时能够使用的内存缓冲区的大小