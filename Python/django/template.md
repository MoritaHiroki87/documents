# templateの書き方

## base_templateの書き方

```
{% load staticfiles %}
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE-edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    
    <title>{% if request.path != '/' %}{% block title %}{% endblock %} | {% endif %}JTI Web App</title>
    <meta name="description" content="" />
    <meta name="roobts" content="noindex, nofollow" />
    
    <link href="https://fonts.googleapis.com/css?family=Open+Sans" rel="stylesheet">
    <link rel="shortcut icon" type="image/png" href="{% static 'favicon.ico' %}"/>
    <link rel="apple-touch-icon" sizes="180x180" href="{% static 'apple-touch-icon.png' %}"/>
    
    {% block stylesheet %}{% endblock %}
    
</head>
<body>
<div class="container">
    <header>
        <nav>
            <ul>
                {% if user.is_authenticated %}
                <li><a href="{% url 'logout' %}" class="logout">Logout</a></li>
                {% else %}
                <!-- <li><a href=" url 'accounts:signup' %}" class="signup">Sign up</a></li> django前カッコを削除済み -->
                <li><a href="{% url 'login' %}" class="login">Login</a></li>
                {% endif %}
            </ul>
        </nav>
    </header>
    <div class="content">
        {% block content %}{% endblock %}
    </div>
</div>

</body>
</html>
```

## headerの書き方
```html
{% extends "appname/basehtml.html" %}

{% load staticfiles %}
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="https://fonts.googleapis.com/css?family=Open+Sans" rel="stylesheet">
    <title>title</title>
    <link rel="stylesheet" href="{% static 'appname/cssname.css' %}" />
</head>
<body>
    
    <!-- urlリンク -->
    <a class="postalLink link-icon" href="{% url 'appname:pathname' %}">
    
</body>
</html>

```
pathnameはurls.pyで指定のname属性

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
