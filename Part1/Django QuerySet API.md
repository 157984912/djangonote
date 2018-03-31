# Django templates

> 从数据库中查询出来的结果一般是一个集合，这个集合叫做 QuerySet

1. QuerySet 创建对象的方法
   ```python
   1. Person.objects.create(name='lin')
   2. per = Person(name='lin')
   per.save()
   3.per = Person()
   per.name = 'lin'
   per.save()
   4.Person.objects.get_or_create(name='lin')
   ```