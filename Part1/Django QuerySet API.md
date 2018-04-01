# Django templates

> QuerySet：从数据库中查询出来的一个结果集。

#### QuerySet 创建对象的方法

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

#### 获取对象的方法

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

#### 查询出结果并删除

```python
# 查询出名字中包含"abc"的人，并删除
Person.objects.filter(name__contains='abc').delete()
# 也可以写成
person = Person.objects.filter(name__contains='abc')
person.delete()
```

#### 更新数据

```python
# 查询出名字中包含"abc"的人，并更新为"ABC"
Person.objects.filter(name__contains='abc').update(name="ABC")
```

> get_or_create()和update_or_create()会先检查数据是否存在，速度会慢一点点
>
> QuerySet 是可迭代的，可for循环

!> **注意事项：**

> 如果只是检查 Person 中是否有对象，应该用 Person.objects.all().exists()
>
> 用 len(person) 可以得到Person的数量，但是推荐用 Person.objects.count()来查询数量，后者用的是SQL：SELECT COUNT(*)
>
> list(person) 可以强行将 QuerySet 变成 列表
>
> QuerySet 重复的问题，使用`distinct()`去重

> Author.objects.all() #结果为QuerySet
>
> Author.objects.values_list('name', 'qq') #结果为元组
>
> Author.objects.values('name', 'qq') #结果为字典

!> **注意**

> values_list 和 values 返回的并不是真正的 列表 或 字典，也是 queryset，他们也是 lazy evaluation 的（惰性评估，通俗地说，就是用的时候才真正的去数据库查）
>
>  如果查询后没有使用，在数据库更新后再使用，你发现得到在是新内容！！！如果想要旧内容保持着，数据库更新后不要变，可以 list 一下
>
> 如果只是遍历这些结果，没有必要 list 它们转成列表（浪费内存，数据量大的时候要更谨慎！！！）
