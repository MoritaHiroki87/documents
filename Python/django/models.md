# models.pyの書き方

## 凡例

```python
from django.db import models
import uuid


# Create your models here.
class Project(models.Model):
    class Meta:
        db_table = "project"
        
    ID = models.AutoField(primary_key=True)
    name = models.TextField()
    null_blank = models.TextField(null=True, blank=True)
    min_n_max = models.IntegerField(default=30000,
                                  validators=[validators.MinValueValidator(10000),
                                              validators.MaxValueValidator(100000)])

    def __str__(self):
        return str(self.name)


```

## 設定できるオプション
- ``null``と``blank``: ``null``はDBの空欄、``blank``はフォームの空欄
- ``primary_key``: ``Ture``にすることで主キーにできる。
- ``unique``: ``True``でユニークのみ許可。``DateTimeField``型に関しては``unique_for_date``
- ``default``: デフォルト値の設定。呼び出し可能オブジェクトを取ることもできるので、関数与えたりでいい感じのデフォルト値を設定できる。
- ``db_column``: DBのカラム名を設定する。DBのカラム名をmodelのフィールド名と別にしたいモチベーションってなんなんだろう。
- ``max_length``: 桁数
- ``validators``: バリデーション

## 特殊なフィールド
- ``DecimalField``: デシマルとして保存できる。

## 参考にしたいところ
[Django モデル層](https://qiita.com/sandream/items/494887598bacfc2b244c)  
[Djangoモデルフィールドのnullとblankの違いを理解する](https://djangobrothers.com/blogs/django_null_blank/)   
[バリデータ - Django ドキュメント](https://docs.djangoproject.com/ja/2.2/ref/validators/)   
