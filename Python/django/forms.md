# forms.pyの書き方

```python
from django import forms
from .models import Card

# クラスのフォーム
class ClassForm(forms.ModelForm):
    """フォーム"""
    class Meta:
        model = Card
        fields = {
            'card_name',
            'card_detail',
            'card_order',
        }

# クラスなしのフォーム
class ClassLessForm(forms.Form):
    card_name = forms.CharField(label="カードの名前")
    card_detail = forms.FloatField(label="詳細")

```
