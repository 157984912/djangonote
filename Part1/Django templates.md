# Django templates

1. 在settings.py中加入templates路径，Django 就会找到templates文件夹中的模板文件。
   ```python
   TEMPLATES = [
       {
           'BACKEND': 'django.template.backends.django.DjangoTemplates',
           'DIRS': [os.path.join(BASE_DIR, 'templates')],
           'APP_DIRS': True,
           ...
   ```

2. 网站模板的设计：一般网站分为头部（head），底部（footer），内容（body），自定义（CSS、JS）等

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>{% block title %}默认标题{% endblock %}</title>
       {% block css %}{% endblock %}
   </head>
   <body>
   {% block content %}
   <p>默认内容</p>
   {% endblock %}
    
   {% include 'footer.html' %}
   {% block js %}{% endblock %}
   </body>
   </html>
   ```

   `block`为被重写的部分，`include`为包含其他模版文件的内容，`extends`为继承其他模    版文件的内容，需要写在文件开头位置，如`{% extends 'base.html' %}`

3. 一般来说在模版文件中，使用`{{ 变量 }}`，使用`{% 功能性语句，如条件、循环等 %}`

   ```html
   列表循环：
   {% for i in List1 %}
   	{{ i }}
   {% endfor %}
   ```
4. for循环的一些变量：

   |  变量 | 描述 |
   | :--- | :--- |
   | forloop.counter | 索引从 1 开始算 |
   | forloop.counter0 | 索引从 0 开始算 |
   | forloop.revcounter | 索引从最大长度到 1 |
   | forloop.revcounter0 | 索引从最大长度到 0 |
   | forloop.first | 当遍历的元素为第一项时为真 |
   | forloop.last | 当遍历的元素为最后一项时为真 |
   | forloop.parentloop | 用在嵌套的 for 循环中， 获取上一层 for 循环的forloop |
5. ==, !=, >=, <=, >, <，and, or, not, in, not in等都可以在模版文件中使用 