## 运算符 ##
### 案例目的 ###
创建数据表，对标重的数据进行运算操作。  
创建表tmp15，其中包含VARCHAR类型字段note 和 INT类型字段price。  

### 过程 ###
1、创建表  
<pre>
CREATE TABLE tmp15 (note VARCHAR(100), price INT);
</pre>
2、插入数据

    INSERT INTO tmp15 VALUES ('Apple', 50);
3、对表中的数值进行算术运算，
<pre>

odoo=> SELECT  price,price+10,price-10,price*2,price/2,price%3 FROM tmp15;
 price | ?column? | ?column? | ?column? | ?column? | ?column?
-------+----------+----------+----------+----------+----------
    50 |       60 |       40 |      100 |       25 |        2
(1 row)
</pre>
4、对tmp15中的整数值字段进行比较运算。
<pre>
odoo=> SELECT price,price>10,price<10,price!=10,price=10,price<>10 FROM tmp15;
 price | ?column? | ?column? | ?column? | ?column? | ?column?
-------+----------+----------+----------+----------+----------
    50 | t        | f        | t        | f        | t
</pre>
5、判断price的值是否落在30~80区间，返回与70，30相比最大的值，判断Price是否为列表（10，20，50，35）中的某一个值
<pre>
odoo=> SELECT price,price BETWEEN 30 AND 80, GREATEST(price,70,30), price IN (10,20,50,35) FROM tmp
15;
 price | ?column? | greatest | ?column?
-------+----------+----------+----------
    50 | t        |       70 | t
</pre>
6、对表中的字符串note 进行比较运算，判断是否为空，是否以字母d开头
<pre>
odoo=> SELECT note, note IS NULL,note LIKE 'd%' FROM tmp15;
 note  | ?column? | ?column?
-------+----------+----------
 Apple | f        | f
(1 row)
</pre>
