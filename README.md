# CURSO DE DJANGO
👨‍⚖️DJANGO É UM FRAMEWORK DE DESENVOLVIMENTO WEB EM PYTHON QUE FACILITA A CRIAÇÃO DE APLICATIVOS WEB DE ALTA QUALIDADE.

<img src="FOTO.png" align="center" width="400"> <br>

## CONCEITO:
Django é um framework de desenvolvimento web em Python amplamente utilizado para criar aplicativos web robustos e escaláveis. Aqui estão alguns conceitos iniciais e exemplos de código para você começar:

1. **Configuração Inicial:**
   Para começar a usar o Django, você primeiro precisa instalá-lo. Use o pip para fazer isso:

   ```bash
   pip install django
   ```

2. **Criando um Projeto:**
   No Django, um projeto é a estrutura global do seu aplicativo web. Para criar um projeto, use o comando `django-admin`:

   ```bash
   django-admin startproject nome_do_projeto
   ```

   Isso criará um diretório com o nome do projeto contendo a estrutura inicial.

3. **Criando um Aplicativo:**
   Em Django, um projeto pode conter vários aplicativos. Cada aplicativo é uma parte independente do projeto. Para criar um aplicativo, use o seguinte comando:

   ```bash
   python manage.py startapp nome_do_aplicativo
   ```

4. **Modelos:**
   Os modelos no Django definem a estrutura do banco de dados. Aqui está um exemplo de um modelo para uma lista de tarefas:

   ```python
   from django.db import models

   class Tarefa(models.Model):
       titulo = models.CharField(max_length=200)
       concluida = models.BooleanField(default=False)

       def __str__(self):
           return self.titulo
   ```

5. **Migrações:**
   Após definir os modelos, você precisa criar migrações para criar ou alterar as tabelas no banco de dados:

   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

6. **Administração:**
   O Django inclui um painel de administração que facilita a gestão dos dados do aplicativo. Para usar o admin, registre seus modelos no arquivo `admin.py` do seu aplicativo:

   ```python
   from django.contrib import admin
   from .models import Tarefa

   admin.site.register(Tarefa)
   ```

7. **Views e URLs:**
   As views processam solicitações do cliente e retornam respostas. Você define as URLs que correspondem a essas views no arquivo `urls.py`:

   ```python
   from django.urls import path
   from . import views

   urlpatterns = [
       path('tarefas/', views.lista_tarefas, name='lista_tarefas'),
   ]
   ```

8. **Templates:**
   Os templates permitem que você crie a aparência de suas páginas web. Você pode usar a linguagem de modelo do Django para criar templates dinâmicos.

9. **Controladores (Views):**
   As views controlam a lógica do aplicativo e renderizam os templates. Aqui está um exemplo de uma view que renderiza uma lista de tarefas:

   ```python
   from django.shortcuts import render
   from .models import Tarefa

   def lista_tarefas(request):
       tarefas = Tarefa.objects.all()
       return render(request, 'lista_tarefas.html', {'tarefas': tarefas})
   ```

10. **Templates HTML:**
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

## CARACTERISTICAS:
### POSITIVAS:
1. **Produtividade Elevada:** O Django promove uma abordagem de desenvolvimento rápido e eficiente. Ele fornece uma grande quantidade de funcionalidades prontas, como um sistema de administração, sistema de autenticação e muito mais, economizando tempo na implementação de recursos comuns.

2. **Segurança Integrada:** Django coloca grande ênfase na segurança. Ele inclui proteções contra ameaças comuns, como injeção de SQL e ataques CSRF. Além disso, atualizações de segurança são frequentes.

3. **Documentação Abundante:** O Django possui uma documentação extensa e bem escrita que facilita o aprendizado e o desenvolvimento. Há uma grande comunidade de desenvolvedores que contribui com tutoriais, recursos e soluções.

4. **Padrão de Projeto MVC:** O Django segue o padrão de projeto Model-View-Controller (MVC), que promove a separação clara entre a lógica de negócios (modelos), a apresentação (templates) e o controle (views) do aplicativo.

5. **Extensibilidade:** Você pode estender as funcionalidades do Django através de aplicativos de terceiros (third-party apps) e criar seus próprios aplicativos personalizados.

6. **Sistema de Templates:** O sistema de templates do Django permite criar páginas HTML dinâmicas e reutilizáveis, tornando a construção de interfaces de usuário mais fácil.

### NEGATIVAS:
1. **Curva de Aprendizado Inicial:** Para iniciantes, o Django pode ter uma curva de aprendizado acentuada, especialmente para aqueles que não estão familiarizados com os conceitos de desenvolvimento web e Python.

2. **Complexidade em Projetos Grandes:** À medida que os projetos crescem, a estrutura do Django pode se tornar complexa e difícil de gerenciar. Isso pode exigir uma boa organização e planejamento.

3. **Opiniões Fortes:** O Django tem suas próprias opiniões e abordagens sobre como as coisas devem ser feitas. Isso pode ser uma desvantagem se você desejar flexibilidade total em suas escolhas de bibliotecas ou métodos de implementação.

4. **Requer Conhecimento em Python:** Para usar o Django efetivamente, é necessário ter conhecimento em Python, o que pode ser uma desvantagem se você preferir ou já estiver familiarizado com outras linguagens.

5. **Alto Uso de Recursos em Alguns Casos:** Em projetos muito grandes ou com alta demanda de tráfego, o Django pode consumir mais recursos do que algumas alternativas mais leves, o que pode requerer otimização adicional.

## SUBSIDIOS:
- [CURSO CRIADO PELO "MATHEUS BATTISTI - HORA DE CODAR"](https://youtube.com/playlist?list=PLnDvRpP8BnewqnMzRnBT5LeTpld5bMvsj&si=G4YKIOWKFgpP6PM2)
- [CURSO FEITO PELO VILHALVA](https://github.com/VILHALVA)
- [VEJA A DOCUMENTAÇÃO](https://docs.djangoproject.com/en/4.2/)
- [LINGUAGEM DE PROGRAMAÇÃO](https://github.com/VILHALVA/CURSO-DE-PYTHON)

