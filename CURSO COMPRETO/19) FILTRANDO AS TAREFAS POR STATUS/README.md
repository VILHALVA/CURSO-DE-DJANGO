# FILTRANDO AS TAREFAS POR STATUS
Para filtrar tarefas por status (concluídas ou não concluídas) em um projeto Django, você pode seguir estas etapas:

**1. Crie uma View para Listar Tarefas por Status:**

Primeiro, crie uma view que permita aos usuários filtrar as tarefas por status. Você pode criar uma view que aceita um parâmetro de consulta na URL para especificar o status desejado. Por exemplo:

```python
from django.shortcuts import render
from .models import Task

def listar_tarefas(request, status):
    if status == 'concluidas':
        tarefas = Task.objects.filter(concluida=True)
    elif status == 'nao-concluidas':
        tarefas = Task.objects.filter(concluida=False)
    else:
        tarefas = Task.objects.all()

    return render(request, 'lista_de_tarefas.html', {'tarefas': tarefas, 'filtro_status': status})
```

Neste exemplo, a view `listar_tarefas` aceita um parâmetro `status` que pode ser `'concluidas'`, `'nao-concluidas'` ou qualquer outra coisa. Com base no valor desse parâmetro, a view filtra as tarefas usando `Task.objects.filter()`.

**2. Configure URLs para Filtrar Tarefas:**

Em seu arquivo `urls.py`, configure as URLs para acessar a view de filtro de tarefas. Você pode usar parâmetros de consulta na URL para especificar o status desejado. Por exemplo:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('tarefas/', views.listar_tarefas, {'status': 'todas'}, name='todas_tarefas'),
    path('tarefas/concluidas/', views.listar_tarefas, {'status': 'concluidas'}, name='tarefas_concluidas'),
    path('tarefas/nao-concluidas/', views.listar_tarefas, {'status': 'nao-concluidas'}, name='tarefas_nao_concluidas'),
]
```

Neste exemplo, criamos três URLs para listar todas as tarefas, listar tarefas concluídas e listar tarefas não concluídas.

**3. Adicione Links no Template:**

No seu template, adicione links ou botões que permitam aos usuários filtrar as tarefas. Por exemplo:

```html
<a href="{% url 'todas_tarefas' %}">Todas as Tarefas</a>
<a href="{% url 'tarefas_concluidas' %}">Tarefas Concluídas</a>
<a href="{% url 'tarefas_nao_concluidas' %}">Tarefas Não Concluídas</a>
```

Isso permite que os usuários escolham o status das tarefas que desejam visualizar.

**4. Exiba o Status Atual no Template:**

No seu template de lista de tarefas, exiba o status atual (Todas as Tarefas, Tarefas Concluídas, Tarefas Não Concluídas) para que os usuários saibam qual filtro está sendo aplicado. Por exemplo:

```html
<h1>{{ filtro_status|capfirst }} Tarefas</h1>
```

Neste exemplo, usamos o filtro `capfirst` para capitalizar a primeira letra do status.

Com essas etapas, você pode permitir que os usuários filtrem as tarefas por status em seu projeto Django. Lembre-se de adaptar a implementação ao design e aos requisitos específicos do seu aplicativo.