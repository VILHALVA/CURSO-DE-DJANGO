# PAGINAÇÃO
A paginação é uma técnica usada em aplicativos da web para dividir grandes conjuntos de dados em partes menores, chamadas páginas, tornando mais fácil para os usuários navegar e visualizar esses dados. No contexto do Django, a paginação é frequentemente usada para lidar com grandes conjuntos de resultados de consulta de banco de dados e exibi-los em várias páginas.

Aqui estão as etapas para implementar a paginação em um projeto Django:

**1. Configurar a Paginação:**

A paginação no Django é implementada por meio de classes e funções no módulo `django.core.paginator`. Primeiro, você precisa importar essas classes no seu aplicativo.

```python
from django.core.paginator import Paginator
```

**2. Paginar os Dados:**

Suponhamos que você tenha uma lista de objetos ou uma consulta que deseja paginar. Você pode usar a classe `Paginator` para paginar esses dados. Por exemplo:

```python
from django.core.paginator import Paginator

# Suponha que 'lista_de_itens' seja a lista que você deseja paginar
paginator = Paginator(lista_de_itens, itens_por_pagina)

# 'itens_por_pagina' é o número de itens por página que você deseja exibir
```

**3. Acessando Páginas Específicas:**

Para acessar uma página específica, você pode usar o método `get_page` do objeto `Paginator`. Por exemplo, para acessar a página 2:

```python
pagina = paginator.get_page(2)
```

**4. Usar Páginas no Template:**

Agora, você pode passar a página desejada para o seu template e exibir os itens nessa página. No seu template, você pode acessar os itens da página como uma lista e iterar sobre eles. Aqui está um exemplo:

```html
<ul>
    {% for item in pagina %}
        <li>{{ item.nome }}</li>
    {% endfor %}
</ul>
```

**5. Adicionar Controles de Navegação:**

Normalmente, é uma prática comum adicionar controles de navegação para permitir que os usuários naveguem entre as páginas. Isso pode ser feito com links para a página anterior e a página seguinte, bem como links para páginas específicas. Você pode usar os atributos `has_previous`, `has_next`, `previous_page_number` e `next_page_number` do objeto `Paginator` para criar esses controles.

**Exemplo de Template com Controles de Navegação:**

```html
{% if pagina.has_previous %}
    <a href="?page={{ pagina.previous_page_number }}">Anterior</a>
{% endif %}
<span>Página {{ pagina.number }} de {{ pagina.paginator.num_pages }}.</span>
{% if pagina.has_next %}
    <a href="?page={{ pagina.next_page_number }}">Próxima</a>
{% endif %}
```

**6. Configurar a Quantidade de Itens por Página:**

Você pode definir a quantidade de itens exibidos por página configurando a variável `itens_por_pagina` ao criar o objeto `Paginator`.

**7. Configurar a URL com o Parâmetro de Página:**

Certifique-se de que a URL que acessa a página inclua um parâmetro para indicar o número da página. Por exemplo, você pode usar `?page=2` na URL para acessar a página 2.

Com essas etapas, você pode implementar a paginação em seu projeto Django para lidar com grandes conjuntos de dados e fornecer uma experiência de usuário mais amigável ao navegar e visualizar esses dados. Lembre-se de que a implementação exata pode variar dependendo das necessidades do seu projeto e do uso de modelos e consultas específicos.