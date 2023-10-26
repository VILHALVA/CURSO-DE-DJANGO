# ESTENDENDO TEMPLATES E TEMPLATE BASE PARA O PROJETO
Estender templates e criar um "template base" é uma prática comum no desenvolvimento web com Django. Isso permite que você crie um layout comum para todas as páginas do seu site e, em seguida, estenda esse layout com templates específicos para cada página. Aqui está como você pode fazer isso:

**1. Criando o Template Base:**

Primeiro, crie um template base que servirá como o layout comum para todas as páginas do seu site. Este template conterá elementos que devem aparecer em todas as páginas, como o cabeçalho, menu de navegação, rodapé, etc.

Suponha que você crie um arquivo chamado `base.html` no diretório de templates do seu aplicativo. Aqui está um exemplo simplificado de `base.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}Título Padrão{% endblock %}</title>
</head>
<body>
    <header>
        <!-- Seu cabeçalho aqui -->
    </header>
    <nav>
        <!-- Seu menu de navegação aqui -->
    </nav>

    <div class="conteúdo">
        {% block content %}
        {% endblock %}
    </div>

    <footer>
        <!-- Seu rodapé aqui -->
    </footer>
</body>
</html>
```

Observe os blocos `{% block %}` no código acima. Eles indicam áreas que podem ser substituídas em templates que estendem `base.html`.

**2. Estendendo o Template Base:**

Agora, para criar uma página específica que utiliza o layout do `base.html`, você pode estender o template base. Por exemplo, suponha que você queira criar uma página de "Sobre Nós". Crie um arquivo `sobre.html` no mesmo diretório de templates do seu aplicativo e estenda o `base.html` da seguinte forma:

```html
{% extends "base.html" %}

{% block title %}Sobre Nós{% endblock %}

{% block content %}
    <h1>Sobre Nós</h1>
    <p>Este é o conteúdo da página "Sobre Nós".</p>
{% endblock %}
```

A linha `{% extends "base.html" %}` indica que este template está estendendo o `base.html`, enquanto os blocos `{% block %}` substituem o título e o conteúdo específico para a página "Sobre Nós".

**3. Incluindo Páginas no Seu Aplicativo:**

Em suas views, você pode renderizar as páginas estendidas com o `base.html`. Por exemplo, em sua view `sobre`, você pode fazer o seguinte:

```python
from django.shortcuts import render

def sobre(request):
    return render(request, 'sobre.html')
```

Isso renderizará a página "Sobre Nós" com o layout definido em `base.html`.

**4. Personalizando Outras Páginas:**

Você pode seguir o mesmo padrão para criar e estender outros templates específicos para diferentes páginas do seu site, mantendo um layout consistente em todo o projeto.

Essa abordagem facilita a manutenção do layout e a consistência visual em seu site. Quando você precisa fazer alterações no cabeçalho, rodapé ou em elementos comuns, basta atualizar o `base.html`, e as mudanças serão refletidas em todas as páginas que estendem o template base.