# MODELS E MIGRATIONS
Os modelos (models) e as migrações são componentes essenciais em um projeto Django. Os modelos são responsáveis por definir a estrutura dos dados que serão armazenados no banco de dados, enquanto as migrações são usadas para criar ou modificar a estrutura do banco de dados de acordo com as definições dos modelos. Vou explicar como criar modelos e executar migrações em um projeto Django:

**1. Criando Modelos:**

Os modelos são criados em um aplicativo Django no arquivo `models.py`. Cada modelo representa uma tabela no banco de dados e define os campos e relacionamentos dessa tabela. Aqui está um exemplo simples de um modelo que representa uma lista de tarefas:

```python
from django.db import models

class Tarefa(models.Model):
    titulo = models.CharField(max_length=200)
    descricao = models.TextField()
    concluida = models.BooleanField(default=False)

    def __str__(self):
        return self.titulo
```

Neste exemplo, criamos um modelo `Tarefa` com três campos: `titulo`, `descricao` e `concluida`. O campo `titulo` é uma string de no máximo 200 caracteres, `descricao` é um campo de texto e `concluida` é um campo booleano que indica se a tarefa está concluída ou não.

**2. Criando Migrações:**

Após definir os modelos, é necessário criar migrações para que o Django crie as tabelas correspondentes no banco de dados ou faça alterações na estrutura do banco de dados. Para criar migrações, use o seguinte comando:

```bash
python manage.py makemigrations
```

Isso examinará os modelos definidos em seu aplicativo e gerará um arquivo de migração no diretório `migrations` do seu aplicativo. O arquivo de migração contém instruções para criar ou modificar as tabelas do banco de dados.

**3. Aplicando Migrações:**

Após criar as migrações, você deve aplicá-las ao banco de dados com o seguinte comando:

```bash
python manage.py migrate
```

Isso executará as migrações pendentes e criará ou modificará as tabelas no banco de dados de acordo com os modelos definidos.

**4. Usando o Admin do Django:**

Uma maneira conveniente de interagir com os modelos e os dados no banco de dados é através do sistema de administração do Django. Para isso, você precisa registrar os modelos no arquivo `admin.py` do seu aplicativo. Por exemplo:

```python
from django.contrib import admin
from .models import Tarefa

admin.site.register(Tarefa)
```

Depois de registrar um modelo, você pode acessar o sistema de administração em `http://127.0.0.1:8000/admin/` (seu servidor de desenvolvimento deve estar em execução) e gerenciar os dados do modelo, incluindo adicionar, editar e excluir registros.

**5. Trabalhando com Dados:**

Agora que você tem modelos e migrações configurados, pode criar, recuperar, atualizar e excluir dados do banco de dados usando o Django. Por exemplo, para criar uma nova tarefa:

```python
nova_tarefa = Tarefa(titulo="Minha nova tarefa", descricao="Descrição da tarefa", concluida=False)
nova_tarefa.save()
```

Para recuperar todas as tarefas não concluídas:

```python
tarefas_nao_concluidas = Tarefa.objects.filter(concluida=False)
```

Essas são as etapas básicas para criar modelos e executar migrações em um projeto Django. À medida que você desenvolve seu aplicativo, pode criar modelos adicionais e executar migrações conforme necessário para refletir as mudanças na estrutura de dados. O Django facilita a interação com bancos de dados e a criação de aplicativos com funcionalidades de banco de dados robustas.