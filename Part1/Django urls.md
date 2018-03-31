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
    # Django2.0前后有差别，name为别名，可以在模版中使用{% url "add"%}
    path(r'^add/(\d+)/(\d+)/$', app01_views.add2, name='add'),
    path('add/<int:a>/<int:b>/', app01_views.add, name='add'),
]
```

