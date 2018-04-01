# Django urls

```python
# Django2.0以前from django.urls import url
from django.conf.urls import path
from django.conf.urls import include
from django.contrib import admin
from app01 import views as app01_views

urlpatterns = [
    path('admin/', admin.site.urls),
    # include路由分发，包含miniAPP下的urls
    path('mini/', include('mini.urls')),
    path('login/', app01_views.acc_login),
    path('logout/', app01_views.acc_logout, name="logout"),
    # Django2.0前后有差别，name为别名，可以在模版中使用{% url "add" 参数1 参数2%}
    path(r'^add/(\d+)/(\d+)/$', app01_views.add2, name='add'),
    path('add/<int:a>/<int:b>/', app01_views.add, name='add'),
]
```

> 模板中使用生成URL {% url 'add' 2012 %}
>
> 函数中使用生成URL reverse('add', args=(2012,)) 路径:django.urls.reverse
>
> Model中使用获取URL 自定义get_absolute_url()方法
