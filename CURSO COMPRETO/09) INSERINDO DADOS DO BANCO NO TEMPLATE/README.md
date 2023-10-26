# INSERINDO DADOS DO BANCO NO TEMPLATE
Para inserir dados do banco de dados em um template no Django, você precisará seguir algumas etapas. Aqui está um guia passo a passo:

**1. Recuperando Dados do Banco de Dados:**

Primeiro, você precisa recuperar os dados do banco de dados que deseja exibir no seu template. Isso pode ser feito em uma view do Django. Por exemplo, suponhamos que você tenha um modelo `Tarefa` que represente tarefas a serem exibidas em uma lista:

```python
from django.shortcuts import render
from .models import Tarefa

def lista_de_tarefas(request):
    tarefas = Tarefa.objects.all()
    return render(request, 'lista_de_tarefas.html', {'tarefas': tarefas})
```

Neste exemplo, recuperamos todas as tarefas do banco de dados usando `Tarefa.objects.all()` e passamos as tarefas como um contexto para o template.

**2. Criando o Template:**

Agora, crie o template onde você deseja exibir os dados do banco de dados. Vamos criar um arquivo `lista_de_tarefas.html` para exibir a lista de tarefas:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Lista de Tarefas</title>
</head>
<body>
    <h1>Lista de Tarefas</h1>
    <ul>
        {% for tarefa in tarefas %}
            <li>{{ tarefa.titulo }}</li>
        {% endfor %}
    </ul>
</body>
</html>
```

Neste template, usamos um loop `{% for %}` para iterar sobre a lista de tarefas e exibimos o título de cada tarefa usando a variável `tarefa.titulo`.

**3. Renderizando o Template:**

Na view `lista_de_tarefas`, usamos a função `render` para renderizar o template e passar as tarefas como contexto. O contexto é um dicionário que contém os dados que você deseja tornar disponíveis no template.

**4. Atualizando URLs:**

Certifique-se de que a URL para a view `lista_de_tarefas` está configurada corretamente em seu arquivo `urls.py`. Por exemplo:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('lista_de_tarefas/', views.lista_de_tarefas, name='lista_de_tarefas'),
]
```

**5. Acessando a Página:**

Acesse a página `http://127.0.0.1:8000/lista_de_tarefas/` em seu navegador (ou a URL correspondente) para visualizar a lista de tarefas recuperada do banco de dados e exibida no template.

Com essas etapas, você pode inserir dados do banco de dados em um template do Django. Lembre-se de que você pode personalizar o template e a formatação de acordo com suas necessidades, além de incluir mais informações e detalhes das tarefas, se necessário.