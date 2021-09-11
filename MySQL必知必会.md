# MySQL必知必会

* 选择数据库：`use 数据库名字;`

___

### ①、show语句

* 显示所有数据库：`show databases;`
* 显示当前选择数据库中的所有表：`show tables;`
* 显示单个表：`show 表名 form 数据库名;`
* 显示服务器状态信息：`show status;`
* 显示创建数据库的语句：`show create database 数据库名;`
* 查看创建表的语句：`show create table 表名;`
* 查看创建视图的语句：`show create view 视图名;`
* 查看存储过程创建语句：`show create procedure 过程名;`
* 显示安装权限：`show grants;`
* 显示错误或警告：`show errors;`和`show warnings;`

---

### ②、select语句

* 检索单个列：`select 列名 from 表名;`[^注1]

* 检索多个列：`select 列名1, 列名2, … from 表名;`

* 检索所有列：`select * from 表名;`

* 检索单个列数据不同的行：`select distinct 列名 from 表名;`

* ==完整的select语句（select语句的子句顺序）==：

  > `select select选项 字段列表 from 数据源[ where 条件 gruop by 分组 having 条件 order by 排序 limit 限制]`
  >
  > * 【必须】from子句（限制检索的位置）:`from 表名`
  >
  > * where子句（指定筛选条件进行过滤行）：`where 筛选条件`
  >
  >   > 范围值检查：`between A and B`
  >   >
  >   > 空值检查：`is null`
  >   >
  >   > 指定值检查：`in 指定值列表`（一般配合子查询使用）
  >   >
  >   > 通配符检查：`like 通配符字段`[^注3] （将会筛选出符合通配符字段的数据，仅包含不会筛选出）
  >   >
  >   > 正则表达式检查：`regexp 正则表达式`（将会筛选出所有包含正则表达式的数据）
  >
  > * group by子句（分组数据）：`group by 检索列或表达式列`
  >
  > * having 子句（指定筛选条件进行过滤行）：`having 筛选条件`
  >
  > * order by子句（规定检索的顺序）：`order by 列名1 [DESC], 列名2 [desc], …`（默认为顺序，desc代表逆序）
  >
  > * limit子句（限制检索的数量）：`limit [从第几行开始, ]数量` [^注2]

* 给字段取别名：`字段 as 别名`

* 调用函数：`函数名(实参列表);`

  > [常用函数](https://www.runoob.com/mysql/mysql-functions.html)
  >
  > 也可以参考*Mysql.md的第十四节函数部分*

* 组合查询：把多个查询语句的结果汇总为一张表

  > 1. 基本语法：
  >
  >    > ~~~mysql
  >    > select 语句
  >    > union[ union选项]
  >    > select 语句;
  >    > ~~~
  >    >
  >    > * `union选项`：（与select选项基本一样）
  >    >   1. `distinct`：（默认）去重
  >    >   2. all：保存所有数据
  >
  > 2. Note：
  >
  >    > 1. union理论上只要保证字段数一样，不要求每次拿到的数据对应的字段类型一致。且永远只保留第一个select语句对应的字段名（原则上还是需要让每个select语句的字段保持一致）
  >    > 2. `order by`语句只能出现一次且只能出现在最后一条SELECT语句中，并将应用于全部结果集

* 联结：在一条select语句中关联多个表

  >1. 等值联结（又称内部联结）
  >
  > ~~~mysql
  >-- 表A中有主键，而表B中有对应的外键
  >SELECT 表A字段, 表B字段
  >FROM 表A, 表B
  >WHERE 表A.主键名 = 表B.外键名;
  >-- INNER JOIN语法（首选规范写法），等效于上方的SELECT语句
  >SELECT 表A字段, 表B字段
  >FROM 表A（主表） INNER JOIN 表B（从表）
  >ON 表A.主键名 = 表B.外键名;
  > ~~~
  >
  > 【注：自联结、自然联结都是特殊的内部联结】
  >
  >2. 自联结（更加高效的子查询）
  >
  > ~~~mysql
  >-- 子查询
  >SELECT prod_id, prod_name
  >FROM products
  >WHERE vend_id = (SELECT vend_id
  >                 FROM products
  >                 WHERE prod_id = 'DTNTR');
  >-- 等效于上方子查询的自联结
  >SELECT p1.prod_id, p2.pord_name
  >FROM products AS p1, products AS p2
  >WHERE p1.vend_id = p2.vend_id
  >  AND p2.vend_id = 'DTNTR';
  > ~~~
  >
  >3. 自然联结
  >
  >   因为如果直接列出所有表中的全部字段会导致出现重复字段，所以我们要列出所以表中的信息的话。只需要对主表使用通配符`*`列出其全部字段，剩下的表使用字段名一一列出即可。事实上，我们迄今为止建立的所有联结都是自然联结，我们很少用到非自然联结。~~（也就是说这玩意没啥P用）~~ 
  >
  >4. 外部联结
  >
  >   使用主表的记录对从表的记录求笛卡尔积，若满足匹配条件则保留，若主表的记录一条记录也没有匹配成功，则从表对应的字段值为NULL
  >
  >~~~mysql
  >--- 左联结
  >SELECT 主表字段, 从表字段
  >FROM 主表 LEFT JOIN 从表
  >ON 联结条件;
  >--- 右联结
  >SELECT 主表字段, 从表字段
  >FROM 从表 RIGHT JOIN 主表(）)
  >ON 联结条件;
  >~~~


---

### ③、全文本搜索

==仅适用于MyISAM搜索引擎==

* 步骤

  > 1. 在表创建语句中使用子句 `FULLTEXT()`包裹要进行全文本搜索的字段
  > 2. 在`where子句`中使用`Match()`指定被搜索的字段（传递给Match的值必须与FULLTEXT中定义的值相同），使用`Against()`指定要搜索的表达式
  > 3. SELECT语句的返回结果中，将根据搜索字段的权值降序

* 其它扩展知识：[MySQL全文本搜索教程]([MySQL 全文搜索 | 新手教程 (begtut.com)](https://www.begtut.com/mysql/mysql-full-text-search.html))

---

### ④、insert语句

* 插入单个行：`insert into 表名[costomers(字段1, 字段2, ……)] values(值1, 值2, …);`

  > 若字段列表指定，值列表需要于字段列表一一对应；若字段列表不指定，值列表需要与表的字段顺序一一对应

* 插入多个行：`insert into 表名[costomers(字段列表)] values(值列表1), (值列表2);`

* 插入检索出的数据：`insert into 待插入表名[costomers(字段列表)] select 值列表 from 表名[ select子句];`

---

### ⑤、update语句

* 更新特定行：`update 表名 set 字段名1 = 新值1[, 字段名2 = 新值2, …] where 限制条件; `

* 更新所有行：`update ignore 表名 set 字段名1 = 新值1[, 字段名2 = 新值2, …];`

  >  删除某一列：可设置它为NULL

---

### ⑥、delete语句

* 删除特定行：`delete from 表名 where 限制条件;`

---

### ⑦、create语句

1. 创建表：`CREATE TABLE`

    ~~~mysql
    CREATE TABLE 新表名
    (
    字段名 字段类型[字段属性],
    字段名 字段类型[字段属性],
    [PRIMARY KEY (字段名)]
    )[表选项];
    ~~~

   > 字段类型：详见*MySQL.md*中的列类型
   >
   > 字段属性：详见*MySQL.md*中的列属性
   >
   > `PRIMARY KEY (字段名)`：设置主键
   >
   > 表选项：`[engine 选择的存储引擎 ][charset 选择的字符集 ][collate 选择的校对集]`
   >
   > > 字符集说明：若是在cmd中执行，选择字符集为gbk；其他情况下，一般选择utf8
   > >
   > > 存储引擎：
   > >
   > > > Innodb：一个可靠的事务处理引擎，但不支持全文本搜索
   > > >
   > > > MyISAM：一个性能极高的引擎，它支持全文本搜索，但不支持事务处理
   > > >
   > > > MEMORY：功能上等同于MyISAM，但是其数据存储在内存，速度特别快，适合存储临时表
   
2. 创建视图：`create view 视图名 as select指令;`

3. 创建存储过程：`create procedure 过程名([参数列表]) begin 过程体 end;`

4. 创建触发器：

    ~~~mysql
    delimiter $$
    create trigger 触发器名字 触发时机 触发事件 on 表 for each row
    begin 
    触发器语句
    end
    $$
    delimiter ;
    ~~~

    > * 触发对象：`on 表 for each row`  => 绑定了表中的每一行，因此当任意一行发生指定操作时，就会触发触发器
    >
    > * 触发时机：表中的每一行都会对应两种不同的状态
    >
    >   > 1. `before`：表中数据发生改变前的状态
    >   > 2. `after`：表中数据已经改变后的状态
    >
    > * 触发事件：mysql中针对的目标是数据发生改变，则对应的操作只有写操作（增删改）
    >
    >   > 1. `insert`：插入
    >   > 2. `update`：更新
    >   > 3. `delete`：删除

---

### ⑧、alter语句

1. 增加列

   `alter table 表名 add 字段名 字段类型; `

2. 删除列

   `alter table 表名 drop column 字段名;`

3. 增加外键

   ~~~mysql
   ALTER TABLE 从表
   ADD [constraint `外键名`]
   FOREIGN KEY(外键字段)
   REFERENCES 主表(主键);
   ~~~
   
4. 更新视图

   `alter view 视图名字 as 新的视图指令;`

   （等效于：`create or replace view 视图名字 as 新的指令;`）

---

### ⑨、drop语句

1. 删除表：`drop table 表名;`
2. 删除视图：`drop view 视图名;`
3. 删除存储过程：`drop procedure 过程名;`
4. 删除触发器：`drop trigger 触发器名;`

---

### ⑩、其它语句

1. 重命名表：`rename table 旧表名1 to 新表名1[, 旧表名2 to 新表名2];`

2. 调用存储过程：`call 过程名([实参列表]);`

3. 游标操作

   > 1. 声明：`declare 游标名 cursor for select语句; `
   >
   > 2. 开启游标：将Fetch指针指向第一个数据
   >
   >    `open 游标名;`
   >
   > 3. Fetch游标：读取Fetch指针指向的数据，并把指针后移（若指针指向NULL，则Fetch游标会报错）
   >
   >    `fetch 游标名 into 变量1[, 变量2, …];`
   >
   > 4. 关闭游标
   >
   >    `close 游标名;`

___

### 【注释部分】

[^注1]: 完全限定的表名：`数据库名.表名`
[^注2]:在MySQL中，0代表false，所以行从1开始
[^注3]: 通配符`%`表示任意数量的字段（0也可以），通配符`_`表示单个字段





