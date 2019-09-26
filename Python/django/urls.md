# urls.pyの書き方

```python
from django.urls import path
from . import views
from .views import *

# config.urls
urlpatterns = [
    # admin
    path('admin/', admin.site.urls),
    # apps
    path('xxx/', include('app_name.urls')), 
    # userいじった時？
    path('accounts/', include('django.contrib.auth.urls')),
]


# app_name.urls
app_name = 'app_name'
urlpatterns = [
    # classView使用時
    path('', ProjectListView.as_view(), name='project_list'),
    path('project/<int:project_id>/', ProjectView.as_view(), name='project'),
    
    # View関数使用時
    # path('kaeseru/', views.kaeseru, name='kaeseru'),
    # path('permission/', views.permission_error, name='permission_error'),
]
```


# メモ
