## kylin创建model与cube

## 概述
> 通过kylin的web管理页面可以进行创建model与cube与操作，在创建model与cube前需要先创建工程(或者选择已经存在的工程)，加载数据源，一个数据源可以建过个model，一个model可以建多个cube

<br/>
<br/>

## 登录kylin管理界面
```html
地址:http://localhost:7070/kylin (默认用户名密码ADMIN/KYLIN)
```

<br/>
<br/>

## 登录后导航页概览
> 登录后web页面主要包含4个模块, Insight, Model, Monitor, System

```html
Insight   查询交互页面,可以对cube创建的数据进行sql查询操作
Model     主要包含model与cube列表，可以对model与cube进行查看与修改
Monitor   cube构建与慢sql查询监控信息展示页面
System    kylin的系统参数信息,可以查询Kylin系统的参数信息和进行修改
```

![web_navigation](https://github.com/chlsmile/note/blob/master/notefile/kylin/navigation/web_navigation.png)

<br/>
<br/>

## 创建工程

#### 1.选择创建工程
![kylin_add_project_index](https://github.com/chlsmile/note/blob/master/notefile/kylin/project/add_project_index.png)

#### 2.填写要创建的工程参数信息
```html
Project Name          不能为空，只能是数字，字母，下划线；在整个系统内需要唯一；创建完成后不允许修改
Project Description   可以为空
```
![kylin_add_new_project](https://github.com/chlsmile/note/blob/master/notefile/kylin/project/add_new_project.png)

<br/>
<br/>


## 加载数据源
> 加载数据源有三种方式，Load Hive Table Metadata， Load Hive Table Metadata From Tree， Add Streaming
```html
- Load Hive Table Metadata (通过手动输入database.table的方式加载hive table metadata)
- Load Hive Table Metadata From Tree(通过选择database.table树的方式加载hive table metadata)
- Add Streaming
```



#### 1.切换到数据源加载标签页
![data_source_index](https://github.com/chlsmile/note/blob/master/notefile/kylin/datasource/data_source_index.png)


#### 2.通过Load Hive Table Metadata From Tree方式加载数据源
![load _hive_table_metadata_from_tree](https://github.com/chlsmile/note/blob/master/notefile/kylin/datasource/load_hive_table_metadata_from_tree.png)


#### 3.数据源加载完成后可以查询到已经加载的数据信息
![view_data_source](https://github.com/chlsmile/note/blob/master/notefile/kylin/datasource/view_data_source.png)

<br/>
<br/>


## 创建model
#### 1.切换到创建model标签页
![add_model_index](https://github.com/chlsmile/note/blob/master/notefile/kylin/model/add_model_index.png)


#### 2.填写model基本信息
```html
Model Name   不能为空，只能是字母，数字，下划线
Description  可以为空
```
![model_designer_model_info](https://github.com/chlsmile/note/blob/master/notefile/kylin/model/model_designer_model_info.png)

#### 3.进入到事实表选择与查找表选择页面
![data_model](https://github.com/chlsmile/note/blob/master/notefile/kylin/model/data_model.png)


#### 4.选择事实表，然后点击添加查找表(每张事实表可以添加多张查找表)
![model_designer_model_add_lookup_table](https://github.com/chlsmile/note/blob/master/notefile/kylin/model/model_designer_model_add_lookup_table.png)

#### 5.查找表设置说明
```html
From Table           可以是事实表也可以是已经设置好的查找表(必须是已经存在了的表)，这个版本的kylin支持雪花模型，不过还是建议使用星型模型
Join Relationship    两张表之间的查询连接关系可以是Inner Join 也可以是Left Join
Select Lookup Table  选择的查找表可以设置别名
New Join Condition   查询连接条件可以是多个
```
![kylin_model_look_table_view](https://github.com/chlsmile/note/blob/master/notefile/kylin/model/model_look_table_view.png)

#### 6.查找表设置样例
![model_designer_model_lookup_table](https://github.com/chlsmile/note/blob/master/notefile/kylin/model/model_designer_model_lookup_table.png)


#### 7.设置完查找表(可以设置多个)后可以查看查找表列表，然后点击next进入到维度设置
![model_designer_model_lookup_table_view](https://github.com/chlsmile/note/blob/master/notefile/kylin/model/model_designer_model_lookup_table_view.png)


#### 8.进行维度设置，然后选择next进行度量设置
![model_designer_model_dimensions](https://github.com/chlsmile/note/blob/master/notefile/kylin/model/model_designer_model_dimensions.png)

#### 9.进行度量设置
![model_designer_select_measure](https://github.com/chlsmile/note/blob/master/notefile/kylin/model/model_designer_select_measure.png)

#### 10.进行分区与数据过滤条件设置,此步完成后即完成了mode的设置
![model_designer_partition_and_filter](https://github.com/chlsmile/note/blob/master/notefile/kylin/model/model_designer_partition_and_filter.png)


## 创建cube

#### 1.切换到Models页签，进行cube创建
![add_cube_index](https://github.com/chlsmile/note/blob/master/notefile/kylin/cube/add_cube_index.png)

#### 2.进行cube基础参数设置
```html
Model Name                 从已经建好model列表中进行选择model 
Cube Name                  不能为空，只能是数字，字母，下划线；在整个系统内需要唯一；创建完成后不允许修改
Notification Email List    通知邮件列表
Notification Events        触发通知的事件，如果通知邮件列表不为空，则Error事件无论设置与否都会触发通知
Description                cube描述可以为空
```
![add_cube_cube_info](https://github.com/chlsmile/note/blob/master/notefile/kylin/cube/add_cube_cube_info.png)

#### 3.进入到维度设置页面
![cube_designer_dimensions_index](https://github.com/chlsmile/note/blob/master/notefile/kylin/cube/cube_designer_dimensions_index.png)


#### 4.进行维度设置
![cube_auto_generate_dimensions](https://github.com/chlsmile/note/blob/master/notefile/kylin/cube/cube_auto_generate_dimensions.png)


#### 5.维度设置列表
![cube_designer_dimensions_list](https://github.com/chlsmile/note/blob/master/notefile/kylin/cube/cube_designer_dimensions_list.png)


#### 6.进入到度量设置页面
![cube_designer_measures_index](https://github.com/chlsmile/note/blob/master/notefile/kylin/cube/cube_designer_measures_index.png)


#### 7.添加度量
![cube_designer_add_measures](https://github.com/chlsmile/note/blob/master/notefile/kylin/cube/cube_designer_add_measures.png)


#### 8.进行度量设置
![cube_designer_add_measures_detail](https://github.com/chlsmile/note/blob/master/notefile/kylin/cube/cube_designer_add_measures_detail.png)


#### 9.完成度量设置
![cube_designer_add_measures_list](https://github.com/chlsmile/note/blob/master/notefile/kylin/cube/cube_designer_add_measures_list.png)


#### 10.设置cube的刷新参数
![cube_designer_refresh_setting](https://github.com/chlsmile/note/blob/master/notefile/kylin/cube/cube_designer_refresh_setting.png)


#### 11.cube高级设置-聚合分组设置
![cube_designer_aggregation_groups](https://github.com/chlsmile/note/blob/master/notefile/kylin/cube/cube_designer_aggregation_groups.png)


#### 11.cube高级设置-Rowkeys设置
![cube_designer_rows_key](https://github.com/chlsmile/note/blob/master/notefile/kylin/cube/cube_designer_rows_key.png)


#### 13.cube高级设置-配置重写
![cube_designer_configuration_overwrites](https://github.com/chlsmile/note/blob/master/notefile/kylin/cube/cube_designer_configuration_overwrites.png)

#### 14.cube设置信息概览
![cube_designer_overview](https://github.com/chlsmile/note/blob/master/notefile/kylin/cube/cube_designer_overview.png)























