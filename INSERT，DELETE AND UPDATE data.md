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

4.
