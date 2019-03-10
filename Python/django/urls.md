# urls.pyの書き方

```python
from django.urls import path
from . import views
from .views import *

app_name = 'app_name'
urlpatterns = [
    # path('app_name以下のurl', ClassView.as_view(), name='逆引きのやつ'),
    path('', ProjectListView.as_view(), name='project_list'),
    path('project/<int:project_id>/', ProjectView.as_view(), name='project'),
    # path('kaeseru/', views.kaeseru, name='kaeseru'),
    # path('permission/', views.permission_error, name='permission_error'),
]
```
