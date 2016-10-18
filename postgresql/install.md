## 安装&示例 ##
1、更新本地apt仓库源，安装postgres package 和 contrib
<pre>
sudo apt-get update
sudo apt-get install postgresql postgresql-contrib
</pre>
2、默认账户postgres，创建role
<pre>
sudo -i -u postgres
main createuser
createuser --interactive
</pre>
![](http://i.imgur.com/FJiq4eS.png)
3、创建一个新用户，一个新数据库，并用新用户连接
<pre>
sudo adduser test1
sudo -i -u postgres
createuser --interactive
createdb test1
sudo -i -u test1
psql -d test1
</pre>
4、查看当前连接信息

    \conninfo
![](http://i.imgur.com/coZ5luE.png)
5、创建和删除表
<pre>
CREATE TABLE table_name (
    column_name1 col_type (field_length) column_constraints,
    column_name2 col_type (field_length),
    column_name3 col_type (field_length)
);
</pre>
<pre>
CREATE TABLE playground (
    equip_id serial PRIMARY KEY,
    type varchar (50) NOT NULL,
    color varchar (25) NOT NULL,
    location varchar(25) check (location in ('north', 'south', 'west', 'east', 'northeast', 'southeast', 'southwest', 'northwest')),
    install_date date
);
\d
</pre>
6、Add,Query,adn Delete in a Table
<pre>
INSERT INTO playground (type, color, location, install_date) VALUES ('slide', 'blue', 'south', '2014-04-28');
INSERT INTO playground (type, color, location, install_date) VALUES ('swing', 'yellow', 'northwest', '2010-08-16');
SELECT * FROM playground;
DELETE FROM playground WHERE type = 'slide';
</pre>
7、在表中增加删除列
<pre>
ALTER TABLE playground ADD last_maint;
ALTER TABLE playground DROP last_maint;
</pre>
8、更新表数据
<pre>
UPDATE playground SET color = 'red' WHERE type = 'swing';
</pre>