# views.pyの書き方

```python
# レンダー関数
from django.shortcuts import render
# クラスビュー
from django.views import View
from django.views.generic import TemplateView, FormView, ListView
# models, forms, servicesなどモジュールの読み込み
from .models import Project, Curtain, Card
from .services import get_card_list_as_json


# ビュー部分
class ProjectListView(View):
    template_name = 'board/project_list.html'

    def get(self, request):
        projects = Project.objects.all()
        context = {'projects': projects}
        return render(request, self.template_name, context)


class ProjectView(View):
    template_name = 'board/project.html'

    def get(self, request, project_id):
        cards = get_card_list_as_json(project_id)
        print(cards)
        project = Project.objects.filter(pk=project_id)

        context = {'cards': cards,
                   'project': project[0]}
        return render(request, self.template_name, context)
        

# Create your views here.
class IndexView(FormView):
    template_name = "myapp/index.html"
    form_class = MyAppForm
    success_url = '/myapp/'
    # initial = {"check_class": 1,} # 初期値
    
    # フォームから入ったデータに色々やりたい時はこちら
    def form_valid(self, form):
        check_class = form.cleaned_data["check_class"]
        int_rate = form.cleaned_data["int_rate"]
        term = form.cleaned_data["term"]
        borrow_amt = form.cleaned_data["borrow_amt"]
        baloon = form.cleaned_data["baloon"]
        int_reduce = form.cleaned_data["int_reduce"]
        int_reduce_term = form.cleaned_data["int_reduce_term"]
        result = calculation(check_class, int_rate, term, borrow_amt, baloon, int_reduce, int_reduce_term)
        context = {
            "form": form,
            "result": "you got!!"
        }
        return render(self.request, "LoanPayment/index.html", context)
        
    # なぜPOSTに対してやってはならんのかという疑問は残る
    def post(self, request, *args, **kwargs):
        form = MyAppForm
        # result = calculation()
        result = request.POST["check_class"] # これはバリデーション済んでない生のデータ
        context = {
            "form": form,
            "result": result,
        }
        print(request.POST)
        return render(request, "myapp/index.html", context)
        
        

class PostView(generic.ListView):
    template_name = 'post_list.html'
    
    # モデルの指定方法はmodel, queryset, get_queryset()の3パターンある。
    model = Post
    def get_queryset(self):
        user = self.request.user # ユーザー情報の取り方はこれ。脈絡ないけど。
        return Post.objects.all()

```

## 参考
[Djangoの汎用ビュー入門（ListView）](https://hombre-nuevo.com/python/python0057/)
