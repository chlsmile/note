## kylin创建model与cube

#### 概述
> 通过kylin的web管理页面可以进行创建model与cube与操作，在创建model与cube前需要先创建工程(或者选择已经存在的工程)，加载数据源

#### 登录kylin管理界面
```html
地址:http://localhost:7070/kylin (默认用户名密码ADMIN/KYLIN)
```

#### 登录后导航页概览
> 登录后web页面主要包含4个模块, Insight, Model, Monitor, System

模块 | 用途
------------- | -------------
Insight  | 查询交互页面,可以对cube创建的数据进行sql查询操作
Model    | 主要包含model与cube列表，可以对model与cube进行查看与修改
Monitor  | cube构建与慢sql查询监控信息展示页面
System   | kylin的系统参数信息,可以查询Kylin系统的参数信息和进行修改

![kylin_web_navigation](https://github.com/chlsmile/note/blob/master/notefile/kylin/navigation/kylin_web_navigation.png)

#### 创建工程

- 选择创建工程
![kylin_add_project_index](https://github.com/chlsmile/note/blob/master/notefile/kylin/project/kylin_add_project_index.png)

- 填写要创建的工程参数信息
```html
Project Name 不能为空，只能是数字，字母，下划线
Project Description可以为空
```
![kylin_add_project_index](https://github.com/chlsmile/note/blob/master/notefile/kylin/project/kylin_add_project_index.png)


#### 加载数据数据源
> 加载数据源有三种方式，Load Hive Table Metadata， Load Hive Table Metadata From Tree， Add Streaming
```html
- Load Hive Table Metadata (通过手动输入database.table的方式加载hive table metadata)
- Load Hive Table Metadata From Tree(通过选择database.table树的方式加载hive table metadata)
- Add Streaming
```

- 通过Load Hive Table Metadata From Tree方式加载数据源
![kylin_add_project_index](https://github.com/chlsmile/note/blob/master/notefile/kylin/project/kylin_add_project_index.png)







