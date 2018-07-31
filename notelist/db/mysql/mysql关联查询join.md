## mysql关联查询join

### join查询语法格式
```mysql
SELECT <row_list>
FROM <left_table>    
<inner|left|right> JOIN <right_table> 
ON <join condition> | USING(column_list)
WHERE   <where_condition>
```

### mysql支持的join类型
- inner join(内连接, 在mysql中join, cross join, inner join是完全等价的)
- left join(左外连接)
- right join(右外连接)
- mysql不支持full join(全连接), 可以通过left join + union(可去除重复数据)+ right join来实现


### join查询的执行顺序如下(SQL语句里第一个被执行的总是FROM子句)：
- FROM:对左右两张表执行笛卡尔积，产生第一张表vt1。行数为n*m（n为左表的行数，m为右表的行数)
- ON:根据ON的条件逐行筛选vt1，将结果插入vt2中

### 测试数据

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


### inner join查询
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

### left join查询
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

### right join查询
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

### union左连接与右连接
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

### cross join
- 交叉连接，得到的结果是两个表的乘积，即笛卡尔积.
- 在mysql cross join 与inner join 的表现是一样的，在不指定 on 条件得到的结果都是笛卡尔积，反之取得两个表完全匹配的结果。
inner join 与 cross join 可以省略 inner 或 cross 关键字
```sql
select p.last_name, p.first_name, o.order_no
from t_person p
cross join t_order o
order by p.last_name

+-----------+------------+----------+
| last_name | first_name | order_no |
+-----------+------------+----------+
| Adams     | John       | 77895    |
| Adams     | John       | 24562    |
| Adams     | John       | 44678    |
| Adams     | John       | 34764    |
| Adams     | John       | 22456    |
| Bush      | George     | 44678    |
| Bush      | George     | 34764    |
| Bush      | George     | 22456    |
| Bush      | George     | 77895    |
| Bush      | George     | 24562    |
| Carter    | Thomas     | 44678    |
| Carter    | Thomas     | 34764    |
| Carter    | Thomas     | 22456    |
| Carter    | Thomas     | 77895    |
| Carter    | Thomas     | 24562    |
+-----------+------------+----------+

```
### TODO 执行顺序
### TODO join查询索引情况分析
