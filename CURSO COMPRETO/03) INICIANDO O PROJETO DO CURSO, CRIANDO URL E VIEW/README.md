# INICIANDO O PROJETO DO CURSO, CRIANDO URL E VIEW
Vamos começar a criar um projeto Django, definir uma URL e uma view. Isso é uma parte fundamental para construir seu aplicativo web Django. Vou guiar você através dos passos:

**1. Criando um Projeto Django:**

Se você ainda não criou um projeto Django, siga as etapas que mencionei anteriormente na seção de Instalação e Configuração para criar um projeto Django. Vou supor que você nomeou seu projeto como `meu_projeto`. Certifique-se de que você está no diretório raiz do seu projeto antes de continuar.

**2. Criando uma Aplicação:**

No Django, a funcionalidade do aplicativo é organizada em "aplicativos". Vamos criar um aplicativo chamado `curso`:

```bash
python manage.py startapp curso
```

Isso criará uma estrutura de diretórios e arquivos para o aplicativo `curso`.

**3. Definindo uma URL:**

Para definir uma URL, você precisará criar um arquivo `urls.py` no diretório do aplicativo `curso`. Dentro deste arquivo, você pode configurar os padrões de URL que mapeiam para as views do seu aplicativo.

Abra o arquivo `urls.py` no diretório `curso` e defina uma URL simples. Vamos criar uma URL que aponta para uma view chamada `minha_view`:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('minhapagina/', views.minha_view, name='minha_view'),
]
```

Aqui, `minhapagina/` é o caminho da URL que irá acionar a view `minha_view`.

**4. Criando uma View:**

Agora, você precisa criar a view `minha_view`. Abra o arquivo `views.py` no diretório `curso` e defina uma função de view simples:

```python
from django.shortcuts import render
from django.http import HttpResponse

def minha_view(request):
    return HttpResponse("Bem-vindo à minha primeira página do Django!")
```

Esta função de view simples retorna uma resposta HTTP com uma mensagem de boas-vindas. Você pode personalizar a lógica da view conforme necessário.

**5. Configurando a URL Raiz do Projeto:**

Para que o Django saiba como lidar com as URLs do aplicativo, você precisa incluir as URLs do aplicativo no arquivo `urls.py` do projeto. Abra o arquivo `urls.py` no diretório raiz do seu projeto e inclua o seguinte:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('curso.urls')),
]
```

O `include('curso.urls')` direcionará as solicitações para as URLs definidas no aplicativo `curso`.

**6. Iniciando o Servidor:**

Agora, você pode iniciar o servidor de desenvolvimento novamente:

```bash
python manage.py runserver
```

Acesse a URL `http://127.0.0.1:8000/minhapagina/` no seu navegador, e você deverá ver a mensagem de boas-vindas da sua view.

Isso é um exemplo simples de como criar uma URL e uma view em um projeto Django. Conforme você avança no curso, você pode adicionar mais views, templates e funcionalidades ao seu aplicativo web.