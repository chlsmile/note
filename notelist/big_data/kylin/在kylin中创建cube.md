## 在kylin中创建cube

#### 登录kylin管理页面
```html
http://localhost:7070/kylin
```

#### 导航页面
![kylin_navigation](https://github.com/chlsmile/note/blob/master/notefile/kylin/kylin_navigation.png)
</br>
</br>

#### 创建工程入口
![kylin_create_project_1](https://github.com/chlsmile/note/blob/master/notefile/kylin/kylin_create_project_1.png)
</br>
</br>

#### 创建工程
- Project Name(工程名)只能是字母，数组，下划线
- Project Description(工程描述信息)为非必填项
![kylin_create_project_2](https://github.com/chlsmile/note/blob/master/notefile/kylin/kylin_create_project_2.png)
</br>
</br>

#### 切换到选择数据源入口
![kylin_choose_data_source_1](https://github.com/chlsmile/note/blob/master/notefile/kylin/kylin_choose_data_source_1.png)

#### 选择数据源(有3种方式)，这里采用Load Hive Table Metadata From Tree的方式
- Load Hive Table Metadata (通过手动输入database.table的方式加载hive table metadata)
- Load Hive Table Metadata From Tree(通过选择database.table树的方式加载hive table metadata)
- Add Streaming

![load_hive_table_from_tree](https://github.com/chlsmile/note/blob/master/notefile/kylin/kylin_choose_data_source_load_hive_table_from_tree.png)
</br>
</br>

#### 数据源树结构列表
![kylin_hive_database](https://github.com/chlsmile/note/blob/master/notefile/kylin/kylin_hive_database.png)
</br>
</br>

#### 选择表并同步数据
![kylin_choose_table_and_sync](https://github.com/chlsmile/note/blob/master/notefile/kylin/kylin_choose_table_and_sync.png)
</br>
</br>

#### 同步元数据成功后可以查看到数据源信息
![kylin_data_souce_view](https://github.com/chlsmile/note/blob/master/notefile/kylin/kylin_data_souce_view.png)
</br>
</br>








