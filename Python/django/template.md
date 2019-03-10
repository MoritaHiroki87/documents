# templateの書き方

## headerの書き方
```html{% load staticfiles %}
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="https://fonts.googleapis.com/css?family=Open+Sans" rel="stylesheet">
    <title>住宅の家賃価値計算ツール</title>
    <link rel="stylesheet" href="{% static 'rentvalue/index.css' %}" />
    <link rel="stylesheet" href="{% static 'rentvalue/form.css' %}" />
</head>
<body>
</body>
</html>

```

### for文で辞書
```html
    {% for curtain_k, curtain_v in cards.items %}
        <p>-----------</p>
        <p>curtain: {{ curtain_k.curtain_name }}</p>
        <p>-----------</p>
        {% for card in curtain_v %}
            <p>card_name: {{ card.card_name }}</p>
            <p>card_id: {{ card.pk }}</p>
        {% endfor %}
    {% endfor %}
```
