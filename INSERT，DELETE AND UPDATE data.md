# 第三章： 更新，删除和插入数据  
1.列属性。  
我们可以查看表的列属性。仅在这里介绍个栏目，  
列名称前面的小黄点表示是主列；type一栏是内容的格式（如int，char，varchar），varchar是可变长度的字符，不会导致空间浪费；extra是如果没有内容是否要赋值。  

2.插入单行。  
使用INSERT INTO 语句，最简单的就是 INSERT INTO customers VALUES（里面填入每一列的内容）。  
如果这样的话，values里面需要写入每一列的内容，如果要使用列的默认值就填DEFAULT，空就可以写NULL。  
你也可以在INSERT INTO语句后面加上括号，变成customers（），在括号里面写不使用默认值的列内容，这样在values内就可以少写一点了     

3.插入多行。  
非常简单，在INSERT INTO shippers（name） VALUE（‘shipper1’）这样是插入单行。  
INSERT INTO shippers（name） VALUE（‘shipper1’），（‘shipper2’），（‘shipper3’）这样就是插入多行了。  

4.插入分层行。  
有时候一个表的一个数据会对应另一个表里的多个数据，这种表叫做子母表。  
插入分层行就是在多个表里插入数据，示例如下：  
INSERT INTO order（customer_id,order_date,status) VALUES(1,'2019-01-01',1)   
INSERT INTO order_items VALUES(LAST_INSERT_ID(),1,1,2.95)   
这里面用到一个mysql的内在函数LAST_INSERT_ID()就是指上一个插入操作插入的最后一个ID值，这样插入的时候两个表的id就能对上了   

5.创建表复制。  
创建表复制这个操作本身很简单，就是使用create table +复制表名称+ as语句即可。  
比如说我要复制一个customers表，就使用CREATE TABLE customers_archive AS SELECT * FROM customers    
这样操作就可以复制一张表了。
USE sql_invoicing;
CREATE TABLE  invoices_archive AS
SELECT inv.invoice_id,inv.number,cli.name AS client,inv.invoice_total,inv.payment_total,inv.invoice_date,inv.payment_date,inv.due_date
FROM invoices inv
JOIN clients cli 
    USING (client_id)
WHERE payment_date IS NOT NULL

6.更新单行。 
使用UPDATE语句。示例如下：  
UPDATE invoices  
SET payment_total=10,payment_date='2019-01-01'    
WHERE invoice_id=1;  
表示将invoice表里id=1的数据更新成set里的内容，当然=右边也可以是表里的数据列的数据并可以进行四则运算payment_date=due_date也是合规的 

7.更新多行。  
和更新单行没什么区别，就是WHERE语句内容变一变。比如我想修改生日在5-1日之前的人，就只修改WHERE语句的内容即可。  
需要注意的只是mysql工作台如果想要更新多行，需要在设置里把safe update勾选去掉才可以，不然会报错。这个设置就是为了防止你不小心修改了不想修改的数据而设置。  

8.在updates语句中使用子查询。  
子查询就像当于两个for循环那个套在里面的循环，先进行查询再以返回值参与到之前的for循环中。  
具体而言就是讲WHERE invoice_id=1这一句改变，比如我们要修改所有orders表里积分大于300的用户的数据，那就这样修改   
WHERE customer_id IN (SELECT customer_id FROM orders WHERE points > 3000)     

9.
