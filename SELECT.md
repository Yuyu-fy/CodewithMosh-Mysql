# 第一章：SELECT语句

首先我们学会调用：
使用 # USE # 语句，用法   
< USE sql_store > 
sql_store是你想要调用的数据库的名称

接下来是SELECT语句，
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

接下来出现的情况是，你不希望显示出来的内容是points+10，那你可以使用如下语句：  
SELECT points+10 AS discout_factor  
当然，如果你希望是中间有空格的几个单词，那么用以下语句：  
SELECT points+10 AS "discout factor"(单引号‘’也可以）

最后一点，如果想在选取用的数据中，去除重复数据，则使用以下语句：  
SELECT DISTINCT state 就可以完成去重    
作业题：  
USE sql_store;
SELECT  name, unit_price , unit_price *1.1 AS "new price"
FROM products;

其次是Where语句。Where会对选取数据进行筛选，设定一个标准然后会一条一条比对，只会输出符合条件的数据  
如：Select * From customers Where prices > 300,SQL中的符号有>,<,>=,<=,!=,=,<>(同！=）  
如果是要等于字符内容，则要对字符内容打上""或者'',值得注意的是字符的大小写并不影响判断，如Where state = ‘va’和 = ‘VA’会得到相同的结果。
同样的，日期虽然是数字，但是在SQL中仍认为是字符，因为包含了-这样的符号，例如Where birth_date > '1900-01-01'
作业题：  
USE sql_store;
SELECT * 
FROM orders
WHERE order_date >= '2019-01-01' and order_date <= '2020-01-01';


