# ADICIONANDO FUNCIONALIDADE DE CONCLUIR TAREFA
Para adicionar a funcionalidade de concluir tarefas em um projeto Django, você pode seguir estas etapas:

**1. Adicionar um Campo "Concluída" ao Modelo de Tarefa:**

Primeiro, adicione um campo booleano ao seu modelo `Task` para rastrear se uma tarefa foi concluída ou não. Por exemplo:

```python
from django.db import models
from django.contrib.auth.models import User

class Task(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    titulo = models.CharField(max_length=200)
    descricao = models.TextField()
    concluida = models.BooleanField(default=False)  # Campo para rastrear o estado da tarefa
```

**2. Criar uma View para Marcar Tarefas como Concluídas:**

Agora, crie uma view que permite aos usuários marcar tarefas como concluídas. Você pode criar uma view que recebe o ID da tarefa como um parâmetro na URL e atualiza o campo `concluida` para `True`. Por exemplo:

```python
from django.shortcuts import redirect
from .models import Task

def marcar_como_concluida(request, tarefa_id):
    tarefa = Task.objects.get(id=tarefa_id)
    tarefa.concluida = True
    tarefa.save()
    return redirect('lista_de_tarefas')  # Redirecione o usuário para a lista de tarefas após a marcação como concluída
```

Certifique-se de configurar a URL para acessar esta view no seu arquivo `urls.py`.

**3. Criar um Botão ou Link para Marcar Tarefas como Concluídas:**

No template que exibe a lista de tarefas, adicione um botão ou link que permita aos usuários marcar uma tarefa como concluída. Por exemplo:

```html
{% for tarefa in tarefas %}
    <li>
        {{ tarefa.titulo }}
        <a href="{% url 'marcar_como_concluida' tarefa.id %}">Marcar como concluída</a>
    </li>
{% endfor %}
```

Quando o usuário clicar no link "Marcar como concluída", a view `marcar_como_concluida` será chamada, marcando a tarefa como concluída no banco de dados.

**4. Opcional: Filtrar Tarefas Concluídas ou Não Concluídas:**

Você também pode fornecer opções para os usuários filtrarem as tarefas concluídas e não concluídas. Isso pode ser feito através de links ou botões no template que alteram a consulta para exibir apenas as tarefas com `concluida=True` ou `concluida=False`.

**5. Exibir Tarefas Concluídas Separadamente:**

Se você deseja exibir tarefas concluídas separadamente das não concluídas, pode criar uma visualização ou template específico para as tarefas concluídas. Isso permite que os usuários vejam as tarefas que já foram concluídas de forma organizada.

Com essas etapas, você pode adicionar a funcionalidade de concluir tarefas em seu projeto Django, permitindo que os usuários marquem tarefas como concluídas e atualizem o estado da tarefa no banco de dados. Isso é útil para aplicativos de lista de tarefas e gerenciamento de tarefas.