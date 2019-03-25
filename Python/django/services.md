# services.pyの書き方（っていうかまあよく書くやつ）
クエリの取り方は下記のページ参照。<br/>
http://thinkami.hatenablog.com/entry/2015/09/04/235841#今回使用するModel



### テーブルをjoin
curtainっていうモデルをprojectとjoinする。<br/>
curtain__projectみたいにアンダーバーふたつで外部キーのやつを引っ張れる。
```python
    cards = Card.objects.filter(curtain__project=project_id).order_by('curtain', 'card_order'
```

### 親子関係のあるデータを扱いやすい辞書型に変換
```python
# output
    {
     "project_id": 1,
     "project_name": "project_1",
     "curtain": [{
        "curtain_id": 1,
        "curtain_name": "curtain_1",
        "card": [{
            "card_id": 1,
            "card_name": "card_1",
            "card_detail": "detail"
            },
            {
            "card_id": 2,
            "card_name": "card_2",
            "card_detail": "detail"
            },
            ...
            ]
        },
        {
        "curtain_id": 2,
        "curtain_name": "curtain_2",
        "card": [{
            "card_id": 1,
            "card_name": "card_1",
            "card_detail": "detail"
            },
            {
            "card_id": 2,
            "card_name": "card_2",
            "card_detail": "detail"
            },
            ...
            ]
        }
        ]
    }
```

```python
# コード
    project = Project.objects.get(pk=project_id)

    project_dic = dict()
    project_dic["project_id"] = project_id
    project_dic["project_name"] = project.project_name

    curtain_list = []
    for curtain in Curtain.objects.filter(project=project).order_by('order', 'pk'):
        curtain_dic = dict()
        curtain_dic["curtain_id"] = curtain.pk
        curtain_dic["curtain_name"] = curtain.curtain_name

        card_list = []
        # cardが存在しないときどう動くのか心配
        for card in Card.objects.filter(curtain=curtain).order_by('card_order', 'pk'):
            card_dic = dict()
            card_dic["card_id"] = card.pk
            card_dic["card_order"] = card.card_order
            card_dic["card_name"] = card.card_name
            card_dic["card_detail"] = card.card_detail
            card_list.append(card_dic)

        curtain_dic["card_list"] = card_list
        curtain_list.append(curtain_dic)

    project_dic["curtain_list"] = curtain_list


```
