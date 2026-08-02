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
  
2.跨数据库连接   
有些时候我们希望将两个或几个不同数据库里的数据表进行连接，这时候我们就需要用到这个语法。  
非常简单，我们只需要在费当前引用数据库的表前面加上它所属数据库的前缀即可，示例如下：  
USE sql_store;  
SELECT *  
FROM order_items oi  
JOIN sql_inventory.products p ON oi.product_id = p.product_id;  

3.自连接  
有时候我们需要将表和表自己相连接，这和跨数据库连接没什么不同，只是使用缩写成为了必需品，否则将无法区分自相连接的表1和表2.  
示例如下：  
USE sql_hr;  
SELECT e.employee_id,e.first_name,m.first_name AS manager  
FROM employees e  
JOIN employees m ON e.reports_to = m.employee_id;

4.多表连接。
很多时候将好几张表连接在一起都是很常见的事情，他的操作也很简单，就是要连接几张表，就写几次JOIN语句即可。  
示例如下：  
USE sql_invoicing;  
SELECT p.date,p.invoice_id,p.amount,c.name,pm.name   
FROM payments p   
JOIN clients c ON p.client_id = c.client_id    
JOIN payment_methods pm ON p.payment_method = pm.payment_method_id;

5.复合连接条件。
在一些情况下，一个数据表中单一数据列会有重复的数值，不能特征地代表一个数据点，所以我们需要将几列一起看才能确定唯一一个数据点，所以我们在将这种表连接的时候需要将几列的数据一起纳入ON 语句中，示例如下：  
USE sql_store;  
SELECT *   
FROM order_items oi    
JOIN order_item_notes oin ON oi.order_id= oin.order_id AND oi.product_id = oin.product_id;

6.隐式连接语法。
即不写join，将on语句写到where语句中，示例如下：  
USE sql_store;  
SELECT order_id,oi.order_id,quantity,oi.unit_price  
FROM order_items oi , products p 
WHRER oi.product_id = p.product_id;   
效果和写JOIN是一样的

7.外连接  
分为LEFT JOIN和RIGHT JOIN，LEFT JOIN 会将先出现的表的数据全部输出，无论是否满足ON条件。RIGHT JOIN则会将后出现的表的数据全部输出，无论是否满足ON条件。  
很简单，给个示例如下：  
USE sql_store;  
SELECT p.product_id,p.name,oi.quantity   
FROM products p   
LEFT JOIN order_items oi ON p.product_id= oi.product_id;

8.多表外连接   
很简单，就进行LEFT JOIN 或者 RIGHT JOIN 的叠加就行。但是建议尽可能只使用LEFT JOIN这样表连接起来更清晰，可读性更高   
示例如下：  
USE sql_store;  
SELECT o.order_date,o.order_id,c.first_name,sh.name AS shipper,oss.name AS status   
FROM orders o    
LEFT JOIN customers c ON o.customer_id = c.customer_id   
LEFT JOIN shippers sh ON o.shipper_id = sh.shipper_id   
LEFT JOIN order_statuses oss ON o.status = oss.order_status_id;
