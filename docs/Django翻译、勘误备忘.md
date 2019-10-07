#Django翻译备忘  

## 2019年10月1日16:32:17  
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

## 2019年10月2日19:50:04  
[所在网页](https://docs.djangoproject.com/zh-hans/2.2/topics/db/models/)
manage.py startapp 命令创建了一个应用结构，包含一个 models.py 文件。若你有很多木星，用独立的文件管理它们会很实用。
**change**
manage.py startapp 命令创建了一个应用结构，包含一个 models.py 文件。若你有很多 modles ，用独立的文件管理它们会很实用。  

## 2019年10月3日16:24:02  
[所在网页](https://docs.djangoproject.com/en/2.2/topics/db/aggregation/)
使用 annotate() 子句来生成每一个对象汇总。
**change**
使用 annotate() 子句 可以生成每一个对象的汇总。


# Django勘误备忘  

## Time：2019年10月3日16:04:02  
* Version：Django version 2.2  
* Reference Link：[模型和数据库-聚合-output_field关键字参数](https://docs.djangoproject.com/zh-hans/2.2/topics/db/aggregation/)  


```python
# 定义Book模型这里，price属性的类型是DecimalField类型
class Book(models.Model):
    name = models.CharField(max_length=300)
    pages = models.IntegerField()
    price = models.DecimalField(max_digits=10, decimal_places=2)
    rating = models.FloatField()
    authors = models.ManyToManyField(Author)
    publisher = models.ForeignKey(Publisher, on_delete=models.CASCADE)
    pubdate = models.DateField()
# 在“速查表”中，使用output_field关键字参数
# Difference between the highest priced book and the average price of all books.
from django.db.models import FloatField
Book.objects.aggregate(
	price_diff=Max('price', output_field=FloatField()) - Avg('price'))
# 应该输出：{'price_diff': 46.85}
# 实际上报错，并提示：django.core.exceptions.FieldError: Expression contains mixed types. You must set output_field
# 因为，output_field 是可选参数，代表返回值的末型字段，需要注意！
# Django文档提示：When combining multiple field types, Django can only determine the output_field if all fields are of the same type. Otherwise, you must provide the output_field yourself.
# 所以，设置output_field=DecimalField()

```

##Time：2019年10月7日14:10:42  
* Version：Django version 2.2  
* Reference Link：[模型和数据库-管理器-自定义管理器-基础管理器](https://docs.djangoproject.com/zh-hans/2.2/topics/db/managers/)  

```text
有一段话：
在关联模型上执行查询时不会使用基础管理器。例如，若 来自教程 的模型 Question 有个 deleted 字段，还有一个基础管理器，用于筛选出 deleted=True 的实例。由 Choice.objects.filter(question__name__startswith='What') 返回的查询结果集会包含关联至已删除的问题的选项。

其中，Choice.objects.filter(question__name__startswith='What')报错：
raise FieldError('Related Field got invalid lookup {}'.format(lookups[0]))
由教程前面所定义的模型来看，
改成，Choice.objects.filter(question__question_text__startswith='What')
```

##Time：2019年10月7日14:50:47  
* Version：Django version 2.2  
* Reference Link：[模型和数据库-管理器-自定义管理器-管理器调用自定义 QuerySet 方法](https://docs.djangoproject.com/zh-hans/2.2/topics/db/managers/)  
```python
class Person(models.Model):
    first_name = models.CharField(max_length=50)
    last_name = models.CharField(max_length=50)
    role = models.CharField(max_length=1, choices=[('A', _('Author')), ('E', _('Editor'))])
    people = PersonManager()
'''其中choices=[('A', _('Author')), ('E', _('Editor'))]改成choices=[('A', ('Author')), ('E', ('Editor'))],因为模型字段的choices字段选项的格式为：
YEAR_IN_SCHOOL_CHOICES = [
    ('FR', 'Freshman'),
    ('SO', 'Sophomore'),
    ('JR', 'Junior'),
    ('SR', 'Senior'),
    ('GR', 'Graduate'),
]
'''
```
