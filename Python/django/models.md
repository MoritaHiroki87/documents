# models.pyの書き方

```python
from django.db import models


# Create your models here.
class Project(models.Model):
    """
    プロジェクト
    project_name:プロジェクト名
    created_at:作成日時
    updated_at:更新日時
    """
    """
    class Meta:
        db_table = "project"
    """

    project_name = models.CharField(max_length=32)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

"""
    def __str__(self):
        return str(self.pattern_num)
"""


```


参考にしたいところ
[Django モデル層](https://qiita.com/sandream/items/494887598bacfc2b244c)
