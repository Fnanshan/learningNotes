Django翻译备忘  

2019年10月1日16:32:17  
[所在网页](https://docs.djangoproject.com/zh-hans/2.2/topics/db/queries/)

跨关系查询¶
Django 提供了一种强大而直观的方式来“追踪”查询中的关联关系  
**change**
Django 提供了一种强大而直观的方式来“追踪”查询中的关系  

要跨越关系，只需跨模型使用关联字段名，字段名由双下划线分割，直到拿到想要的字段。  
**change**
为了跨越关系，只需跨模型使用相关字段的字段名  

本例检索出所有的 Entry 对象，带有 name 为 'Beatles Blog' 的 Blog:
**change**
这个例子检索出了所有的 Entry 对象，其 Blog 的 name 是 'Beatles Blog'  

由于多个条目能同时关联至一个 Blog，两种查询都是可行的，且在某些场景下非常有用。
**change**
由于多个 Entry 能同时关联至一个 Blog，两种查询都是可行的，且在某些场景下非常有用。  

在之前的例子中，我们已经构建过的筛选器都是将模型字段值与常量做比较
**change**
在之前的例子中，我们已经构建过的 filter 都是将模型字段值与常量做比较  

F() 的实例充当查询字段的引用
**change**
F()的实例充当查询中的模型字段的引用  

2019年10月2日19:50:04
[所在网页](https://docs.djangoproject.com/zh-hans/2.2/topics/db/models/)
manage.py startapp 命令创建了一个应用结构，包含一个 models.py 文件。若你有很多木星，用独立的文件管理它们会很实用。
**change**
manage.py startapp 命令创建了一个应用结构，包含一个 models.py 文件。若你有很多 modles ，用独立的文件管理它们会很实用。