# models.pyの書き方

## 凡例

```python
from django.db import models
import uuid


# Create your models here.
class Project(models.Model):
    class Meta:
        db_table = "project"
        
    name = models.TextField()
    null_blank = models.TextField(null=True, blank=True)

    def __str__(self):
        return str(self.name)


```

## 設定できるオプション
- ``primary_key``: ``Ture``にすることで主キーにできる。
- ``unique``: ``True``でユニークのみ許可。``DateTimeField``型に関しては``unique_for_date``
- ``default``: デフォルト値の設定。呼び出し可能オブジェクトを取ることもできるので、関数与えたりでいい感じのデフォルト値を設定できる。

## 特殊なフィールド
- ``DecimalField``: デシマルとして保存できる。

## 参考にしたいところ
[Django モデル層](https://qiita.com/sandream/items/494887598bacfc2b244c)  
[Djangoモデルフィールドのnullとblankの違いを理解する](https://djangobrothers.com/blogs/django_null_blank/)   
