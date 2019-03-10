# services.pyの書き方（っていうかまあよく書くやつ）
クエリの取り方は下記のページ参照。<br/>
http://thinkami.hatenablog.com/entry/2015/09/04/235841#今回使用するModel



### テーブルをjoin
curtainっていうモデルをprojectとjoinする。<br/>
curtain__projectみたいにアンダーバーふたつで外部キーのやつを引っ張れる。
```python
    cards = Card.objects.filter(curtain__project=project_id).order_by('curtain', 'card_order'
```
