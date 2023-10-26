# FOREIGNKEY ENTRE USER E TASK
Para criar uma relação `ForeignKey` entre o modelo de usuário (User) embutido do Django e um modelo de tarefa (Task), siga estas etapas:

**1. Definir o Modelo de Tarefa:**

Primeiro, defina o modelo de tarefa em seu aplicativo. O modelo de tarefa deve incluir um campo de chave estrangeira que se relaciona com o modelo de usuário embutido `User`. Além disso, você pode adicionar outros campos para representar as informações da tarefa. Por exemplo:

```python
from django.db import models
from django.contrib.auth.models import User  # Importe o modelo User embutido

class Task(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    titulo = models.CharField(max_length=200)
    descricao = models.TextField()
    concluida = models.BooleanField(default=False)
```

Neste exemplo, a tarefa está relacionada com um usuário por meio do campo `user`, que é uma chave estrangeira para o modelo `User`. O argumento `on_delete=models.CASCADE` garante que, quando um usuário é excluído, todas as tarefas relacionadas a esse usuário também são excluídas.

**2. Criar e Aplicar Migrações:**

Após definir o modelo de tarefa, crie e aplique migrações para atualizar o banco de dados com as alterações no modelo. Execute os seguintes comandos:

```bash
python manage.py makemigrations
python manage.py migrate
```

**3. Criar Tarefas para um Usuário:**

Agora, você pode criar tarefas para um usuário específico vinculando-as ao usuário por meio do campo `user`. Por exemplo:

```python
# Suponhamos que você tenha um usuário chamado "usuario" (substitua pelo nome real)
usuario = User.objects.get(username='usuario')

# Crie uma nova tarefa vinculada ao usuário
nova_tarefa = Task(user=usuario, titulo="Minha primeira tarefa", descricao="Esta é uma tarefa de exemplo.", concluida=False)
nova_tarefa.save()
```

Isso criará uma tarefa associada ao usuário especificado.

**4. Consultar Tarefas de um Usuário:**

Para recuperar as tarefas de um usuário específico, você pode fazer uma consulta ao modelo `Task` usando o campo `user`. Por exemplo, para recuperar todas as tarefas de um usuário:

```python
usuario = User.objects.get(username='usuario')
tarefas_do_usuario = Task.objects.filter(user=usuario)
```

Isso recuperará todas as tarefas associadas ao usuário "usuario".

Com essas etapas, você pode criar uma relação `ForeignKey` entre o modelo de usuário e o modelo de tarefa no Django e associar tarefas a usuários específicos. Isso é útil para criar aplicativos onde os usuários podem ter tarefas ou itens relacionados a eles.