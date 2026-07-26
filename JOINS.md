# 第二章： JOINS连接
Everybody,I'm back!   
1.JOIN分为内连接和外连接，这里我们先学的是INNNER JOIN。  
Join的作用是将两张表和二唯一，通过ON 语句选择合并标准     
其实整体语法比较简单，我们就先选用作业题的代码并对其进行解答：  
USE sql_store;  
SELECT order_id,oi.order_id,quantity,oi.unit_price  
FROM order_items oi  
JOIN products p ON oi.product_id = p.product_id;  
1）我们先选取的表会在合并后展示在前几列，被合并的表的数据会在后几列出现。  
2）ON语句表达选取合并的标准，如这段程序最后会将product_id相等的数据合并。  
3）我们可以在表名出现后写入他的缩写，如oi和p。这样写代码更加方便，但是要注意的是，一旦给表名命名了缩写，在程序的任何地方都必须以缩写形式写入这个表，包括SELECT语句。
  
2.
