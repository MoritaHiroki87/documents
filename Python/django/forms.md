# forms.pyの書き方
django公式
[https://docs.djangoproject.com/ja/2.1/topics/forms/]



```python
from django import forms
from .models import Card

# モデルありのフォーム
class ClassForm(forms.ModelForm):
    """フォーム"""
    class Meta:
        model = Card
        fields = {
            'card_name',
            'card_detail',
            'card_order',
        }

# モデルなしのフォーム
class ClassLessForm(forms.Form):
    card_name = forms.CharField(label="カードの名前")
    card_detail = forms.FloatField(label="詳細")

```
