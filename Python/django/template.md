# templateの書き方


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
