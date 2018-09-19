## kylin创建model与cube

#### 概述
> 通过kylin的web管理页面可以进行创建model与cube与操作，在创建model与cube前需要先创建工程(或者选择已经存在的工程)，加载数据源

#### 登录kylin管理界面
```html
地址:http://localhost:7070/kylin (用户名ADMIN/密码KYLIN)
```

### 登录后导航页概览
- Insight 查询交互页面
- Model 主要包含model与cube列表
- Monitor cube构建与慢查询监控信息
- System Kylin的系统参数信息
![kylin_web_navigation](https://github.com/chlsmile/note/blob/master/notefile/kylin/navigation/kylin_web_navigation.png)

### 创建工程
#### 1)选择创建工程
![kylin_add_project_index](https://github.com/chlsmile/note/blob/master/notefile/kylin/project/kylin_add_project_index.png)

#### 2)填写要创建的工程参数信息
- Project Name 不能为空，只能是数字，字母，下划线
- Project Description可以为空
![kylin_add_project_index](https://github.com/chlsmile/note/blob/master/notefile/kylin/project/kylin_add_project_index.png)


### 加载数据数据源
> 加载数据源有三种方式，Load Hive Table Metadata， Load Hive Table Metadata From Tree， Add Streaming
- Load Hive Table Metadata (通过手动输入database.table的方式加载hive table metadata)
- Load Hive Table Metadata From Tree(通过选择database.table树的方式加载hive table metadata)
- Add Streaming

#### 1



#### 1)通过Load Hive Table Metadata From Tree方式加载数据源
![kylin_add_project_index](https://github.com/chlsmile/note/blob/master/notefile/kylin/project/kylin_add_project_index.png)







