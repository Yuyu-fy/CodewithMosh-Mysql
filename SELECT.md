# 第一章：SELECT语句

1.首先我们学会调用：
使用 # USE # 语句，用法   
< USE sql_store > 
sql_store是你想要调用的数据库的名称

2.接下来是SELECT语句，
SELECT 后面+要选取的栏目，如SELECT customers_id。如果要选取所有的栏目，则使用*。如SELECT *
后面用FROM语句，表达从哪个数据表中选取数据。如FROM customers
WHERE语句在如果有特定的要求则会用到。比如我只想选取customer_id是1的数据，则WHRER customers_id=1
最后如果有对排序的需求，则用到ORDER BY语句。比如我想按照姓氏排序，则写到ORDER BY first_name  
特殊的	对语句添加注释的方法是在语句前面写-- （注意，--后一定要加空格）   

由于如果使用*调取全部数据会导致调用数据过多产生卡顿，所以通常直接写出需要调用的部分，如：  
SELECT first_name,last_name  

另外，也可以在SELECT语句中完成对数值的修改，如调用一栏整数数据points：
SELECT points，points + 10   
会发现在第二列中的数据比第一列大10  

3.接下来出现的情况是，你不希望显示出来的内容是points+10，那你可以使用如下语句：  
SELECT points+10 AS discout_factor  
当然，如果你希望是中间有空格的几个单词，那么用以下语句：  
SELECT points+10 AS "discout factor"(单引号‘’也可以）

最后一点，如果想在选取用的数据中，去除重复数据，则使用以下语句：  
SELECT DISTINCT state 就可以完成去重    
作业题：  
USE sql_store;
SELECT  name, unit_price , unit_price *1.1 AS "new price"
FROM products;

4.其次是Where语句。Where会对选取数据进行筛选，设定一个标准然后会一条一条比对，只会输出符合条件的数据  
如：Select * From customers Where prices > 300,SQL中的符号有>,<,>=,<=,!=,=,<>(同！=）  
如果是要等于字符内容，则要对字符内容打上""或者'',值得注意的是字符的大小写并不影响判断，如Where state = ‘va’和 = ‘VA’会得到相同的结果。
同样的，日期虽然是数字，但是在SQL中仍认为是字符，因为包含了-这样的符号，例如Where birth_date > '1900-01-01'
作业题：  
USE sql_store;
SELECT * 
FROM orders
WHERE order_date >= '2019-01-01' and order_date <= '2020-01-01';  
  
5.紧接着是AND，OR，NOT语句。如其词义，很好理解就是在判断中加入和，或，整体否定，这里就不做特别说明了。只需知道AND的优先级高于OR即可，不过最好还是对判断式进行完全括号化来增加程序可读性。    
作业题：  
USE sql_store;
SELECT * 
FROM order_items
WHERE  order_id = 6 AND unit_price *quantity > 30;

6.接着是IN语句，这是一个简便的语句，用来替换一些冗长的表达。  
由于计算机中AND 这种逻辑符号前后要连接相同类型的语句，所以如果我们想筛选住在三个州里的人，我们得这么写：  
WHRER state = 'VA' OR state = 'GA' OR state= 'FL'   
显然并不简便，那我们就使用IN语句，使用方法如下：  
WHERE state (NOT) IN （'VA','GA','FL')  
根据需求决定是否添加NOT，括号中扩着的就是我们希望包含的数据条件，大大提升了代码简便性  
作业题：  
USE sql_store;
SELECT * 
FROM order_items
WHERE  quantity  IN (49 , 38 , 72);

7.BETWEEN语句，目的也是简化程序，很好理解就是直接将一个值的区间替换，举个例子就很清晰了：  
WHRER points BETWEEN 1000 AND 3000 等同于 WHERE points >= 1000 AND points <=3000    
但值得注意的是，between不止适用于数字，也适用于字符等形式
作业题：
USE sql_store;
SELECT * 
FROM customers
WHERE  birth_date BETWEEN '1990-01-01' AND '2020-01-01';

8.LIKE语句，一个很有年代感的语句  
用于筛选特定的数据点，有两种语法 % 和 _  
%表示任意个字符，_表示单个字符  具体用法如下：  
WHRER last_name LIKE '%b%'表达名字中有b就行。
LIKE '%b'表示b结尾，前面随便 LIKE '_b'表示就俩字符，前一个随便，后一个是b。
注意，同上面几条中的内容，大写小写不做区分  
作业题：  
1.USE sql_store;
SELECT * 
FROM customers
WHERE  address LIKE '%trail%'  or address LIKE '%avenue';  
2.WHRER phone LIKE '%9'
