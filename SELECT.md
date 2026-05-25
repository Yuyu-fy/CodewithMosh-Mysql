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
