# ADICIONADO CSS, JS E BOOTSTRAP
Adicionar CSS, JavaScript e Bootstrap a um projeto Django é uma etapa importante para melhorar a aparência e a funcionalidade do seu site. Aqui estão as etapas para incluir CSS, JavaScript e Bootstrap no seu projeto:

**1. Adicionando Arquivos Estáticos:**

No Django, arquivos como CSS, JavaScript e imagens são considerados arquivos estáticos. Eles devem ser armazenados em um diretório separado e configurados corretamente no projeto. Vamos seguir as práticas recomendadas para adicionar esses arquivos:

- Crie um diretório chamado "static" no diretório do seu aplicativo. Por exemplo, se você tem um aplicativo chamado "curso", crie um diretório "static" em "curso/static/". A estrutura de diretórios ficaria semelhante a esta:

    ```
    meu_projeto/
    ├── curso/
    │   ├── static/
    │   │   ├── curso/
    │   │   │   ├── css/
    │   │   │   ├── js/
    │   │   │   ├── img/
    ```

- Dentro do diretório "static", você pode criar subdiretórios para organizar seus arquivos. Por exemplo, "css" para arquivos CSS, "js" para arquivos JavaScript e "img" para imagens.

**2. Configurando os Arquivos Estáticos:**

Para que o Django saiba onde encontrar os arquivos estáticos, você precisa configurar as configurações do projeto. No arquivo `settings.py` do seu projeto, adicione o seguinte código:

```python
# settings.py

# ...

# Configurar a pasta raiz dos arquivos estáticos
STATIC_URL = '/static/'

# Adicionar caminho para os diretórios de arquivos estáticos
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'curso/static'),
]

# ...
```

Isso define a pasta raiz de arquivos estáticos como "/static/" e especifica onde o Django deve procurar os arquivos estáticos.

**3. Adicionando Bootstrap:**

Para adicionar o Bootstrap ao seu projeto Django, você tem algumas opções:

- **Baixar o Bootstrap:** Você pode baixar o Bootstrap diretamente do site oficial (https://getbootstrap.com/) e incluir os arquivos CSS e JavaScript no diretório "static" do seu aplicativo.

- **Usar o BootstrapCDN:** Uma maneira fácil de adicionar o Bootstrap é através do BootstrapCDN. Basta adicionar os links para os arquivos CSS e JavaScript no seu template HTML. Por exemplo, em um arquivo `sobre.html`:

```html
{% extends "base.html" %}

{% block title %}Sobre Nós{% endblock %}

{% block content %}
    <h1>Sobre Nós</h1>
    <p>Este é o conteúdo da página "Sobre Nós".</p>
{% endblock %}

<!-- Adicione os links para o BootstrapCDN -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
```

Lembre-se de que o BootstrapCDN é uma opção conveniente, mas pode exigir uma conexão à internet para carregar os arquivos.

**4. Incluindo CSS e JavaScript Personalizados:**

Você pode incluir seus próprios arquivos CSS e JavaScript nos templates do Django da mesma maneira que o Bootstrap, por meio de links ou scripts.

Por exemplo, para adicionar um arquivo CSS personalizado, você pode fazer o seguinte no seu template HTML:

```html
{% block content %}
    <link rel="stylesheet" href="{% static 'curso/css/meu_estilo.css' %}">
    <!-- Conteúdo da sua página -->
{% endblock %}
```

Certifique-se de que o caminho para o arquivo CSS corresponda ao diretório de arquivos estáticos que você configurou.

**5. Coletando Arquivos Estáticos:**

Após adicionar arquivos estáticos, você precisará coletá-los em um diretório específico antes de implantar seu projeto em produção. Use o seguinte comando para coletar os arquivos estáticos:

```bash
python manage.py collectstatic
```

Isso copiará todos os arquivos estáticos de todos os aplicativos em um diretório central para que o servidor da web possa servi-los.

Com essas etapas, você deve ser capaz de adicionar CSS, JavaScript e Bootstrap ao seu projeto Django e personalizar a aparência e a funcionalidade do seu site. Certifique-se de seguir as práticas recomendadas para organização de arquivos estáticos e configurar corretamente as configurações do projeto.