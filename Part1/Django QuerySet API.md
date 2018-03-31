# Django templates

> QuerySet：从数据库中查询出来的一个结果集。

1. QuerySet 创建对象的方法
   ```python
   1. Person.objects.create(name='abc')
   2. per = Person(name='abc')
   per.save()
   3.per = Person()
   per.name = 'abc'
   per.save()
   # 返回一个元组(object, True/False)，创建时返回 True, 已经存在时返回 False
   4.Person.objects.get_or_create(name='abc')
   ```
2. 获取对象的方法
   ```python
   # 查询所有，可切片，不支持负索引
   Person.objects.all()[:10]
   # 获取单条结果，条件结果有多条会报错
   Person.objects.get(name='abc')
   # 获取符合条件的多条结果
   Person.objects.filter(name='abc')
   # name严格等于"abc"，不明白和上一个有什么区别???
   Person.objects.filter(name__exact='abc')
   # 不区分大小，Abc，aBc...
   Person.objects.filter(name__iexact='abc')
   # 包含"abc"的
   Person.objects.filter(name__contains='abc')
   # 包含"abc"，且不区分大小写
   Person.objects.filter(name__icontains='abc')
   # 正则查询，如以abc开头
   Person.objects.filter(name__regex='abc')
   # 正则查询，如以abc开头，并不区分大小写
   Person.objects.filter(name__iregex='abc')
   # 排除name包含"abc"的
   Person.objects.exclude(name__contains="abc")
   # 找出名字含有abc, 但是排除年龄是23岁的
   Person.objects.filter(name__contains='abc').exclude(age='23')
   ```
3. 查询出结果并删除
   ```python
   # 查询出名字中包含"abc"的人，并删除
   Person.objects.filter(name__contains='abc').delete()
   # 也可以写成
   person = Person.objects.filter(name__contains='abc')
   person.delete()
   ```
4. 更新数据
   ```python
   # 查询出名字中包含"abc"的人，并更新为"ABC"
   Person.objects.filter(name__contains='abc').update(name="ABC")
   ```
5. get_or_create()和update_or_create()会先检查数据是否存在，速度会慢一点点
6. QuerySet 是可迭代的，可for循环
!> 注意事项：
!> 如果只是检查 Person 中是否有对象，应该用 Person.objects.all().exists()