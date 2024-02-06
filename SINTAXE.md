# SINTAXE
1. **Modelos:**
   Os modelos no Django definem a estrutura do banco de dados. Aqui está um exemplo de um modelo para uma lista de tarefas:

   ```python
   from django.db import models

   class Tarefa(models.Model):
       titulo = models.CharField(max_length=200)
       concluida = models.BooleanField(default=False)

       def __str__(self):
           return self.titulo
   ```

2. **Administração:**
   O Django inclui um painel de administração que facilita a gestão dos dados do aplicativo. Para usar o admin, registre seus modelos no arquivo `admin.py` do seu aplicativo:

   ```python
   from django.contrib import admin
   from .models import Tarefa

   admin.site.register(Tarefa)
   ```

3. **Views e URLs:**
   As views processam solicitações do cliente e retornam respostas. Você define as URLs que correspondem a essas views no arquivo `urls.py`:

   ```python
   from django.urls import path
   from . import views

   urlpatterns = [
       path('tarefas/', views.lista_tarefas, name='lista_tarefas'),
   ]
   ```

4. **Controladores (Views):**
   As views controlam a lógica do aplicativo e renderizam os templates. Aqui está um exemplo de uma view que renderiza uma lista de tarefas:

   ```python
   from django.shortcuts import render
   from .models import Tarefa

   def lista_tarefas(request):
       tarefas = Tarefa.objects.all()
       return render(request, 'lista_tarefas.html', {'tarefas': tarefas})
   ```

5. **Templates HTML:**
    Você pode criar templates HTML para exibir os dados em suas páginas. Aqui está um exemplo simples:

    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <title>Lista de Tarefas</title>
    </head>
    <body>
        <h1>Minha Lista de Tarefas</h1>
        <ul>
            {% for tarefa in tarefas %}
                <li>{{ tarefa.titulo }}</li>
            {% endfor %}
        </ul>
    </body>
    </html>
    ```
6. **Templates em Django:**
   Em Django, os templates são arquivos HTML que permitem a incorporação de código Python para gerar conteúdo dinâmico. Eles permitem separar o design e a lógica de negócios, facilitando a manutenção e o desenvolvimento de aplicativos da web. Aqui está uma visão geral de como os templates funcionam em Django:

    1. **Sintaxe**:
    - Os templates em Django usam uma sintaxe específica para incorporar código Python. As partes dinâmicas do conteúdo são delimitadas por chaves duplas `{{ }}` para expressões e por chaves `{% %}` para tags de controle.
    - Por exemplo, `{{ variavel }}` é usado para exibir o valor de uma variável, enquanto `{% if condição %} ... {% endif %}` é usado para estruturas condicionais.

    2. **Contexto**:
    - Os templates são renderizados com base em um contexto, que é um dicionário Python contendo os dados a serem exibidos no template.
    - O contexto pode incluir variáveis, objetos e até mesmo funções que podem ser chamadas dentro do template.

    3. **Herança de Templates**:
    - O Django suporta herança de templates, permitindo que você defina um template base comum e estenda ou substitua seções específicas em templates filhos.
    - Isso promove a reutilização de código e facilita a manutenção de uma aparência consistente em todo o aplicativo.

    4. **Filtros**:
    - Os filtros são funções embutidas em Django que permitem modificar ou formatar dados antes de serem exibidos no template.
    - Por exemplo, `{{ texto|lower }}` exibe o texto em minúsculas, enquanto `{{ data|date:"Y-m-d" }}` formata a data.

    5. **Tags de Controle**:
    - As tags de controle permitem a execução de lógica de negócios mais complexa dentro do template, como estruturas de controle (`if`, `for`, etc.) e inclusão de outros templates.
    - Por exemplo, `{% for item in lista %} ... {% endfor %}` itera sobre uma lista e exibe o conteúdo para cada item.

    6. **Comentários e Escapes**:
    - O Django suporta comentários dentro dos templates usando a sintaxe `{# comentário #}`.
    - Além disso, o Django possui uma função de escape automático para evitar ataques XSS (Cross-Site Scripting), o que significa que qualquer conteúdo dinâmico é automaticamente escapado por padrão.

    7. **Uso nos Views**:
    - Nos views do Django, você renderiza um template fornecendo o nome do template e um contexto opcional.
    - Por exemplo, `return render(request, 'meu_template.html', {'variavel': valor})` renderiza o template `meu_template.html` com o contexto fornecido.

    8. **Localização de Templates**:
    - Por padrão, o Django procura por templates dentro do diretório `templates` em cada aplicativo e também no diretório `templates` na raiz do projeto.

