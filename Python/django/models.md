# models.pyの書き方

## 凡例

```python
from django.db import models
import uuid


class Book(models.Model):
    HARDCOVER = 1
    PAPERBACK = 2
    EBOOK = 3
    BOOK_TYPES = (
        (HARDCOVER, 'Hardcover'),
        (PAPERBACK, 'Paperback'),
        (EBOOK, 'E-book'),
    )
    id = models.AutoField(primary_key=True)
    # primary_keyは自動インクリメントさせたいならAutoFieldで設定する。インクリメントの法則を自由にしたい場合はdefautに関数与えるとかする。
    title = models.CharField(max_length=50)
    publication_date = models.DateField(null=True)
    
    author = models.ForeignKey(Author, on_delete=models.PROTECT)
    price = models.DecimalField(max_digits=5, decimal_places=2)
    pages = models.IntegerField(blank=True, null=True)
    book_type = models.PositiveSmallIntegerField(choices=BOOK_TYPES)
    min_n_max = models.IntegerField(default=30000,
                                  validators=[validators.MinValueValidator(10000),
                                              validators.MaxValueValidator(100000)])

    class Meta:
        verbose_name = 'book'
        verbose_name_plural = 'books'
        
    def __str__(self):
        return str(self.name)
        
class Author(models.Model):
    name = models.CharField(max_length=30, blank=True)
        
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
[PostgreSQL specific model fields ArrayField](https://docs.djangoproject.com/ja/2.2/ref/contrib/postgres/fields/#arrayfield)   
