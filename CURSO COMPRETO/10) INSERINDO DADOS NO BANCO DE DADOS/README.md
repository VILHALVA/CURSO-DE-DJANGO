# INSERINDO DADOS NO BANCO DE DADOS
Para inserir dados no banco de dados em um projeto Django, você normalmente seguirá as seguintes etapas:

**1. Definir o Modelo (Model):**

Certifique-se de que você tenha um modelo (model) definido em seu aplicativo Django. O modelo é responsável por definir a estrutura dos dados que serão armazenados no banco de dados. Por exemplo, considere um modelo simples para representar tarefas:

```python
from django.db import models

class Tarefa(models.Model):
    titulo = models.CharField(max_length=200)
    descricao = models.TextField()
    concluida = models.BooleanField(default=False)
```

Este modelo define uma tabela chamada `Tarefa` com três campos: `titulo`, `descricao` e `concluida`.

**2. Criar um Objeto do Modelo:**

Para inserir dados no banco de dados, você precisa criar um objeto do modelo. Por exemplo, para criar uma nova tarefa:

```python
nova_tarefa = Tarefa(titulo="Minha primeira tarefa", descricao="Esta é uma tarefa de exemplo.", concluida=False)
```

**3. Salvar o Objeto no Banco de Dados:**

Depois de criar o objeto do modelo, você deve salvá-lo no banco de dados usando o método `save()`:

```python
nova_tarefa.save()
```

Após a execução do método `save()`, a tarefa será adicionada ao banco de dados.

**4. Exemplo de Inserção de Dados em uma View:**

Você pode criar uma view que execute a inserção de dados no banco de dados. Por exemplo:

```python
from django.shortcuts import render
from .models import Tarefa

def criar_tarefa(request):
    nova_tarefa = Tarefa(titulo="Minha primeira tarefa", descricao="Esta é uma tarefa de exemplo.", concluida=False)
    nova_tarefa.save()
    return render(request, 'sucesso.html')
```

Neste exemplo, a view `criar_tarefa` cria uma nova tarefa e a salva no banco de dados. Em seguida, redireciona o usuário para uma página de sucesso.

**5. Configurando a URL:**

Certifique-se de configurar a URL para acessar a view que cria a tarefa. No arquivo `urls.py` do seu aplicativo:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('criar_tarefa/', views.criar_tarefa, name='criar_tarefa'),
]
```

Agora, quando um usuário acessar a URL `http://127.0.0.1:8000/criar_tarefa/` (ou a URL correspondente que você configurou), a tarefa será criada e inserida no banco de dados.

**6. Acessando o Admin do Django (opcional):**

Outra maneira de inserir dados no banco de dados é através do sistema de administração do Django. Para fazer isso, você pode acessar a interface de administração em `http://127.0.0.1:8000/admin/` (se o servidor de desenvolvimento estiver em execução) e adicionar novos registros ao modelo `Tarefa` diretamente por meio da interface.

Com essas etapas, você pode inserir dados no banco de dados em um projeto Django. Lembre-se de que, em um aplicativo real, os dados geralmente são inseridos por meio de formulários ou API de entrada de dados, mas o conceito básico de criação de objetos do modelo e salvamento no banco de dados permanece o mesmo.