## mysql关联查询join


#### 一、join查询的通用结构
```mysql
SELECT <row_list>
FROM <left_table>    
<inner|left|right> JOIN <right_table> 
ON <join condition>
WHERE   <where_condition>
```

#### 二、join查询的执行顺序如下(SQL语句里第一个被执行的总是FROM子句)：
- FROM:对左右两张表执行笛卡尔积，产生第一张表vt1。行数为n*m（n为左表的行数，m为右表的行数)
- ON:根据ON的条件逐行筛选vt1，将结果插入vt2中

#### 三、测试数据

```sql
CREATE table t_person(
	p_id int(10) UNSIGNED not NULL  comment '用户id',
	last_name VARCHAR(50) not null DEFAULT '' comment '名',
	first_name VARCHAR(50) not null DEFAULT '' comment '姓',
	address VARCHAR(100) not null DEFAULT '' comment '地址',
	city VARCHAR(100) not null default '' comment '城市'
) engine=InnoDB default charset=utf8  comment '用户表';

insert into t_person(p_id,last_name,first_name,address,city) VALUES
(1,'Adams','John','Oxford Street', 'London'),
(2,'Bush','George','Fifth Avenue', 'New York'),
(3,'Carter','Thomas','Changan Street', 'Beijing')

CREATE table t_order(
	o_id int(10) UNSIGNED not NULL  comment '订单id',
	order_no VARCHAR(50) not null DEFAULT '' comment '订单号',
	p_id int(10) UNSIGNED not null  comment '用户id'
) engine=InnoDB default charset=utf8  comment '订单表';

insert into t_order(o_id,order_no,p_id) VALUES
(1,'77895',3),
(2,'44678',3),
(3,'22456',1),
(4,'24562',1),
(5,'34764',65)

```


#### 四、inner join查询
```sql
SELECT p.last_name, p.first_name, o.order_no
FROM t_person p
INNER JOIN t_order o
ON p.p_id = o.p_id

+-----------+------------+----------+
| last_name | first_name | order_no |
+-----------+------------+----------+
| Carter    | Thomas     | 77895    |
| Carter    | Thomas     | 44678    |
| Adams     | John       | 22456    |
| Adams     | John       | 24562    |
+-----------+------------+----------+
```

#### 五、left join查询
```sql

select p.last_name, p.first_name, o.order_no
from t_person p
left join t_order o
on p.p_id=o.p_id

+-----------+------------+----------+
| last_name | first_name | order_no |
+-----------+------------+----------+
| Carter    | Thomas     | 77895    |
| Carter    | Thomas     | 44678    |
| Adams     | John       | 22456    |
| Adams     | John       | 24562    |
| Bush      | George     | NULL     |
+-----------+------------+----------+

```

#### 六、right join查询
```sql


select p.last_name, p.first_name, o.order_no
from t_person p
right join t_order o
on p.p_id=o.p_id

+-----------+------------+----------+
| last_name | first_name | order_no |
+-----------+------------+----------+
| Adams     | John       | 22456    |
| Adams     | John       | 24562    |
| Carter    | Thomas     | 77895    |
| Carter    | Thomas     | 44678    |
| NULL      | NULL       | 34764    |
+-----------+------------+----------+


```

#### union左连接与右连接
- MySQL不支持全外连接(FULL JOIN)，所以可以采取关键字UNION来联合左,右。替代方法 left join + union(可去除重复数据)+ right join
```sql
SELECT p.last_name, p.first_name, o.order_no
FROM t_person p
	LEFT JOIN t_order o ON p.p_id = o.p_id
UNION
SELECT p.last_name, p.first_name, o.order_no
FROM t_person p
	RIGHT JOIN t_order o ON p.p_id = o.p_id	

+-----------+------------+----------+
| last_name | first_name | order_no |
+-----------+------------+----------+
| Carter    | Thomas     | 77895    |
| Carter    | Thomas     | 44678    |
| Adams     | John       | 22456    |
| Adams     | John       | 24562    |
| Bush      | George     | NULL     |
| NULL      | NULL       | 34764    |
+-----------+------------+----------+	

```


#### TODO 执行顺序
#### TODO 不通类型的join图形表示
#### TODO mysql支持的几种join查询(mysql不支持full join， 但可以通过left join union left join来变相实现)
#### TODO 索引情况分析
