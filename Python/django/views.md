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

```
