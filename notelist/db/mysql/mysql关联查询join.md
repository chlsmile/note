## mysql关联查询join

### join的执行顺序

#### 以下是JOIN查询的通用结构：
```mysql
SELECT <row_list>
FROM <left_table>    
<inner|left|right> JOIN <right_table> 
ON <join condition>
WHERE   <where_condition>
```
#### 它的执行顺序如下(SQL语句里第一个被执行的总是FROM子句)：
- FROM:对左右两张表执行笛卡尔积，产生第一张表vt1。行数为n*m（n为左表的行数，m为右表的行数)
- ON:根据ON的条件逐行筛选vt1，将结果插入vt2中
