# services.pyの書き方（っていうかまあよく書くやつ）

### テーブルをjoin
curtainっていうモデルをprojectとjoinする。<br/>
curtain__projectみたいにアンダーバーふたつで外部キーのやつを引っ張れる。
```python
    cards = Card.objects.filter(curtain__project=project_id).order_by('curtain', 'card_order'
```
