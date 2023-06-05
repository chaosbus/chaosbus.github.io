# 基于MySQL数据库ER设计与生成



## 一、背景

新项目使用数据表时，需要根据整个业务数据的情况，将数据进行拆分、关联。使用ER设计的好处是可以在业务结构设计角度来考虑，忽略具体的建表过程，并且可以方便的修改调整。

## 二、操作流程

> 使用工具：[MySQL Workbench](https://cdn.mysql.com//Downloads/MySQLGUITools/mysql-workbench-community-8.0.33-winx64.msi)（免费）

### 2.1 新建

#### a) 新建Model

![image-20230602174931852](http://static.origins.top/md/image-20230602174931852.png)

#### b) 新建EER

![image-20230602175014392](http://static.origins.top/md/image-20230602175014392.png)

### 2.2 设计编辑

#### a) 添加【Table】

![image-20230602175208833](http://static.origins.top/md/image-20230602175208833.png)

双击【Table】，显示表格的相关信息，可以添加字段并设置字段属性

![image-20230602180405598](http://static.origins.top/md/image-20230602180405598.png)

#### b) 添加【外键】

![image-20230602180447234](http://static.origins.top/md/image-20230602180447234.png)

外键类型为：一对一，一对多，多对多。

点击需要的类型按钮，再依次点击需要建立外键关联的两张表，可以看到两表之间生成一条关系连线。

#### c) 编辑【外键】

自动生成的外键（字段）可能不是我们想要的，可以手动编辑

双击外键表【Table】，点击红框【Foreign Keys】Tab，分别编辑黄框与绿框

![image-20230602181400994](http://static.origins.top/md/image-20230602181400994.png)

### 2.3 生成Table

![image-20230602181635056](http://static.origins.top/md/image-20230602181635056.png)

点击菜单栏【Database】-【Forward Engineer】，依次下一步即可将ER中建立的表生成到对应的数据库中。

在**DBeaver**中连接到该数据库后，查看ER图如下：

![image-20230602181954557](http://static.origins.top/md/image-20230602181954557.png)

