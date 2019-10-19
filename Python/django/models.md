# models.pyの書き方

```python
from django.db import models


# Create your models here.
class Project(models.Model):
    class Meta:
        db_table = "project"
        
    name = models.TextField()
    null_blank = models.TextField(null=True, blank=True)

    def __str__(self):
        return str(self.name)


```


参考にしたいところ
[Django モデル層](https://qiita.com/sandream/items/494887598bacfc2b244c)
[Djangoモデルフィールドのnullとblankの違いを理解する](https://djangobrothers.com/blogs/django_null_blank/)
