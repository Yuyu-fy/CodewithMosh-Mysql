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
