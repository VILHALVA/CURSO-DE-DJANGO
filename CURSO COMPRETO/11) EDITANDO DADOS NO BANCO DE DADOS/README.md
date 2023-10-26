# EDITANDO DADOS NO BANCO DE DADOS
Editar dados no banco de dados em um projeto Django envolve a recuperação do registro existente, a modificação dos campos desejados e o salvamento das alterações. Aqui estão as etapas para editar dados no banco de dados:

**1. Recuperando o Registro a Ser Editado:**

Primeiro, você precisa recuperar o registro que deseja editar. Isso geralmente é feito usando um identificador exclusivo, como o ID do registro. Suponhamos que você deseje editar a tarefa com o ID 1:

```python
tarefa = Tarefa.objects.get(id=1)
```

Essa linha de código recupera a tarefa com o ID 1 do banco de dados.

**2. Modificando os Campos:**

Agora que você tem o registro, pode modificar os campos conforme necessário. Por exemplo, se você deseja alterar o título da tarefa:

```python
tarefa.titulo = "Novo título da tarefa"
```

Você pode fazer alterações em qualquer campo do registro da mesma maneira.

**3. Salvando as Alterações:**

Depois de fazer as alterações desejadas, você deve salvar as alterações no banco de dados usando o método `save()`:

```python
tarefa.save()
```

Isso atualizará o registro no banco de dados com as modificações que você fez.

**Exemplo de Edição de Dados em uma View:**

Aqui está um exemplo de como você pode criar uma view para editar dados em um modelo `Tarefa`:

```python
from django.shortcuts import render, redirect
from .models import Tarefa

def editar_tarefa(request, tarefa_id):
    tarefa = Tarefa.objects.get(id=tarefa_id)
    
    if request.method == "POST":
        # Receba os dados do formulário e atualize os campos da tarefa
        tarefa.titulo = request.POST['novo_titulo']
        tarefa.descricao = request.POST['nova_descricao']
        tarefa.concluida = request.POST.get('concluida', False)
        
        # Salve as alterações
        tarefa.save()
        
        return redirect('lista_de_tarefas')  # Redireciona para a lista de tarefas após a edição

    return render(request, 'editar_tarefa.html', {'tarefa': tarefa})
```

Neste exemplo, a view `editar_tarefa` recupera a tarefa com base no `tarefa_id`, atualiza os campos com os dados do formulário (em uma solicitação POST), e depois salva as alterações. Após a edição, a view redireciona o usuário de volta à lista de tarefas.

**Configurando a URL:**

Certifique-se de configurar a URL para acessar a view de edição. No arquivo `urls.py` do seu aplicativo:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('editar_tarefa/<int:tarefa_id>/', views.editar_tarefa, name='editar_tarefa'),
]
```

Neste exemplo, usamos `<int:tarefa_id>` para capturar o ID da tarefa na URL.

**Criando um Formulário (Opcional):**

Em um aplicativo real, é comum criar um formulário para editar dados, o que torna a edição mais amigável para o usuário. Você pode usar o módulo `forms` do Django para criar formulários e validá-los antes de salvar as alterações.

Com essas etapas, você pode editar dados no banco de dados em um projeto Django. Lembre-se de que, para uma aplicação real, a implementação pode ser mais complexa, dependendo dos requisitos do seu projeto, mas os princípios gerais de recuperação, modificação e salvamento de registros no banco de dados permanecem os mesmos.