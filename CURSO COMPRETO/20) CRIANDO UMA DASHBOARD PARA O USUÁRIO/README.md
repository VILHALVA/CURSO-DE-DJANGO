# CRIANDO UMA DASHBOARD PARA O USUÁRIO
Para criar uma dashboard personalizada para o usuário em um projeto Django, você pode seguir as etapas a seguir. Uma dashboard é uma página que oferece uma visão geral das informações relevantes para o usuário, como tarefas, mensagens, atividades, etc. Neste exemplo, vamos criar uma dashboard simples exibindo tarefas do usuário.

**1. Criar a View da Dashboard:**

Primeiro, crie uma view que renderize a dashboard do usuário. Esta view pode recuperar as informações necessárias, como tarefas, mensagens ou outros dados relevantes para o usuário. No exemplo a seguir, vamos criar uma view que exibe tarefas do usuário.

```python
from django.shortcuts import render
from .models import Task

def dashboard(request):
    # Recupere as tarefas do usuário atual (você deve garantir que o usuário esteja autenticado)
    tarefas = Task.objects.filter(user=request.user)

    return render(request, 'dashboard.html', {'tarefas': tarefas})
```

**2. Configure a URL para a Dashboard:**

Em seu arquivo `urls.py`, configure uma URL para acessar a view da dashboard.

```python
from django.urls import path
from . import views

urlpatterns = [
    # ...
    path('dashboard/', views.dashboard, name='dashboard'),
    # ...
]
```

**3. Crie um Template para a Dashboard:**

Agora, crie um template que represente a dashboard do usuário. Você pode usar HTML, CSS e Django Template Tags para criar a aparência e o layout desejados. Por exemplo:

```html
{% extends "base.html" %}

{% block content %}
    <h1>Dashboard</h1>
    <h2>Tarefas do Usuário</h2>
    <ul>
        {% for tarefa in tarefas %}
            <li>{{ tarefa.titulo }}</li>
        {% endfor %}
    </ul>
{% endblock %}
```

**4. Configurar o Acesso à Dashboard:**

Você deve garantir que apenas usuários autenticados acessem a dashboard. Você pode fazer isso usando o decorador `@login_required` nas views. Por exemplo:

```python
from django.contrib.auth.decorators import login_required

@login_required
def dashboard(request):
    # Sua lógica para a dashboard
```

Isso garantirá que apenas usuários autenticados acessem a dashboard.

**5. Personalização e Adição de Funcionalidades:**

A dashboard pode ser personalizada e estendida de acordo com as necessidades do seu projeto. Você pode adicionar gráficos, notificações, links para outras partes do aplicativo e muito mais.

**6. Adicionar Links de Navegação:**

Finalmente, adicione links de navegação no seu aplicativo para permitir que os usuários acessem a dashboard. Isso pode ser feito, por exemplo, adicionando um link no menu principal do seu site ou no cabeçalho.

Com essas etapas, você pode criar uma dashboard personalizada para o usuário em um projeto Django. Lembre-se de que a personalização da dashboard depende dos requisitos do seu projeto e das informações que você deseja exibir para os usuários.