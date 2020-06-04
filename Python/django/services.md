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

### modelをCSVに落とす

#### 使い方
```
create_model_csv(Model)
```

#### コード
```

# model_to_divt()
# https://stackoverflow.com/questions/21925671/convert-django-model-object-to-dict-with-all-of-the-fields-intact
# modelのフィールド名リストを取得
# https://qiita.com/SATOSHI-G/items/e9bffe018d5a0294a7eb


def create_model_csv(models):
    model_2d_list = create_model_2d_list(models)
    create_csv(models._meta.object_name, model_2d_list)


def create_csv(model_name, model_2d_list):
    # ここフォルダパスは任意に変える
    with open("AppName/export_datum/{}.csv".format(model_name), mode="w") as f:
        writer = csv.writer(f)
        writer.writerows(model_2d_list)


def create_model_2d_list(models):
    model_2d_list = list()
    field_names = get_f_names(models)
    value_2d_list = get_f_values(models, field_names)

    model_2d_list.append(field_names)
    model_2d_list = model_2d_list + value_2d_list

    return model_2d_list


def get_f_names(models):
    meta_fields = models._meta.get_fields()
    print(meta_fields)  # ※1

    ret = list()
    for i, meta_field in enumerate(meta_fields):
        # ここちょっと注意。日時系のデータを弾いてる。
        if (i > 0) and (meta_field.name not in ["create_date", "input_date", ]):
            ret.append(meta_field.name)
    print(ret)  # ※2
    return ret


def get_f_values(models, field_names):
    all_objects = models.objects.all()
    value_2d_list = list()
    for object in all_objects:
        value_list = list()
        dictized_object = model_to_dict(object)
        print("@@@@@@@@@@@@@@@{}",format(dictized_object))
        for f_name in field_names:
            value_list.append(dictized_object[f_name])
        value_2d_list.append(value_list)
    return value_2d_list


```
