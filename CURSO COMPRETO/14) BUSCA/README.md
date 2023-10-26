# BUSCA
Para adicionar uma funcionalidade de busca em um projeto Django, você pode seguir estas etapas:

**1. Definir um Formulário de Busca:**

Crie um formulário que permita aos usuários inserir o termo de busca. Você pode criar um formulário personalizado em um arquivo `forms.py` em seu aplicativo. Por exemplo:

```python
from django import forms

class BuscaForm(forms.Form):
    termo_de_busca = forms.CharField(label='Buscar', max_length=100)
```

**2. Configurar uma View de Busca:**

Crie uma view que lide com a busca. Esta view deve processar os dados enviados pelo formulário de busca e executar a pesquisa no banco de dados. Aqui está um exemplo de uma view de busca:

```python
from django.shortcuts import render
from .models import SeuModelo
from .forms import BuscaForm

def buscar(request):
    if request.method == 'GET':
        form = BuscaForm(request.GET)
        if form.is_valid():
            termo_de_busca = form.cleaned_data['termo_de_busca']
            resultados = SeuModelo.objects.filter(campo_de_busca__icontains=termo_de_busca)
            return render(request, 'resultado_de_busca.html', {'resultados': resultados})
    else:
        form = BuscaForm()
    return render(request, 'pagina_de_busca.html', {'form': form})
```

Nesta view, primeiro verificamos se o formulário foi submetido. Se for uma solicitação GET, exibimos o formulário de busca. Se for uma solicitação POST, processamos o formulário, recuperamos o termo de busca e pesquisamos no banco de dados usando o método `filter` do Django.

**3. Configurar URLs:**

Configure as URLs para acessar a view de busca e os resultados. No arquivo `urls.py` do seu aplicativo, você pode adicionar algo como:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('buscar/', views.buscar, name='buscar'),
    path('resultados/', views.resultados, name='resultados'),  # Crie uma view de resultados, se necessário
]
```

**4. Criar um Template para Exibir Resultados:**

Crie um template para exibir os resultados da busca. Você pode usar o objeto `resultados` passado para o template na view para exibir os resultados de forma formatada.

**Exemplo de Template de Resultados:**

```html
{% extends "base.html" %}

{% block content %}
    <h1>Resultados da Busca</h1>
    <ul>
        {% for resultado in resultados %}
            <li>{{ resultado.campo_de_interesse }}</li>
        {% endfor %}
    </ul>
{% endblock %}
```

**5. Adicionar a Barra de Busca no Template:**

Adicione o formulário de busca ao seu template onde desejar que ele apareça. Por exemplo:

```html
<form method="get" action="{% url 'buscar' %}">
    {{ form.as_p }}
    <button type="submit">Buscar</button>
</form>
```

**6. Processar e Exibir Resultados:**

Quando o usuário submeter o formulário de busca, a view `buscar` processará o termo de busca e exibirá os resultados na página de resultados.

Com essas etapas, você pode adicionar uma funcionalidade de busca ao seu projeto Django. Lembre-se de que este é um exemplo básico, e você pode personalizar e aprimorar a funcionalidade de busca de acordo com as necessidades específicas do seu projeto.