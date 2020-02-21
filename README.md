# simple-mooc-sistema-a-distancia-em-python3
O Simple MOOC visa simplificar o ensino a distância, provendo ferramentas objetivas e de fácil uso para cursos a distância. Em Python 3

ESTE SISTEMA TERÁ AS SEGUINTES FUNCIONALIDADES:

 - Sistema de aulas {criar, editar e remover as aulas organizadas por módulos e associadas há um curso com aulas do youtube, materias para download e quiz}
 - Fórum de dúvidas {fórum aberto simples e separado por categorias, o usuário precisará está logado, para poder responder estes tópicos}
 - Exercícios de submissão {local onde os alunos enviarão arquivos como solução depois que o professor criar o exercício, com validação verificando se o conteúdo do aluno bate com o conteúdo que o professor criou, gerando notas}
 - Sistema de avisos {mural simples de avisos onde o professor cria o aviso e todos alunos recebem este aviso, também criaremos uma opção de comentários, podenedo receber os avisos por email}
 - Sistema de contas (usuários) {O aluno deverá está logado para acessar o seu curso, editar seu perfil}

CONFIGURANDO E ATIVANDO O PYTHON PARA SEU AMBIENTE (SO)

 - PYTHON - https://www.python.org/downloads/
 - PIP - https://pip.pypa.io/en/stable/installing/, é o gerenciador de pacotes do Python

 USAREI O AMBIENTE LINUX/UBUNTU

 Em seu terminal acesse o diretório da sua aplicação coloque nele o get-pip.py e execute o seguinte comando:

    sudo python3 get-pip.py

Após instalar o pip agroa podemos instalar nosso virtual env, que é um ambiente vitual da nossa aplicação python, para maiores informação https://virtualenv.pypa.io/en/latest/installation.html

rode o seguinte comando para instalar sua venv, que serve para isolar sua aplicação.

    python3 -m venv nome_da_sua_venv

    python3 -m venv venv

OBS: foi criado um diretório chamado /venv com vários outros diretórios e arquivos, o principal que acessaremos é:

    /venv/bin/activate

Pois ele ativa nossa virtual env.

Para ativar sua venv basta digitar o seguinte comando

    source  venv/bin/activate

Aparece (venv) no início do seu terminal 

    (venv) desenv01@desenv01-Vostro-3583:~/Documentos/simple-mooc-sistema-a-distancia-em-python3$ 

INSTALANDO, CONFIGURANDO E ATIVANDO O DJANGO

Já temos o python e o ambiente instalado, então vamos instalar o django conforme o link oficial https://www.djangoproject.com/download/

No terminal com o venv ativado basta digitar o seguinte comando:

    pip install django

Execute os seguintes comandos em sequências

    python
    import django
    django.VERSION

Instalando o projeto com alguns utilitários do django, basta executar o seguinte comando

    django-admin.py startproject simplemooc

Foi criado o projeto simplemooc

Estrutura básica do projeto
 - simplemooc
    - simplemooc
        - __init__.py -> quer dizer que este dir é considerado um pacote python
        - asgi.py -> onde fica o core do sistema
        - settings.py -> é o setup do nosso projeto
        - urls.py -> Local onde ficará as urls do projeto
        - wgsi.py -> endpoint da aplicação, não mexeremos neste aquivo
    - manage.py -> arquivo utilitário, vai ajudar a gerenciar o projeto, criar banco de dados, migrações super-usuários, ..., será bastante útil no terminal.

EXECUTANDO O SERVIDOR LOCAL DA MINHA APLICAÇÃO DJANGO

Basta acessar o diretório da sua aplicação (/simplemooc) e executar no terminal o seguinte comando com a sua venv ativa

    python manage.py runserver

CONFIGURANDO O BANCO DE DADOS

Usarei o banco padrão da aplicação django o sqlite3

Passos para configurar o banco de dados

 - acesse o arquivo settings.py, o sqlite3 já vem configurado por padrão
    
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
        }
    }

Mudando a localização

Ainda em settings.py mude as seguintes linhas de código para sua localização

    LANGUAGE_CODE = 'en-us'

    TIME_ZONE = 'UTC'

Mudei para 

    LANGUAGE_CODE = 'pt-br'

    TIME_ZONE = 'America/Sao_Paulo'

Criando as tables padrão do djngo

    python manage.py migrate

OBS: o django e baseado em aplicações e por padrão já vem estas instaladas, então a migrate instala todas as tabelas destas aplicações.

    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
    ]

Por enquanto usaremos este sistema de usuário do django, porém depois modificaremos ele.

CRIANDO O SUPER USUÁRIO

Basta rodar o seguinte comando e colocar suas credenciais
    
    python manage.py createsuperuser

ACESSANDO A APLICAÇÃO DO SISTEMA

Basta executar o server

     python manage.py runserver

Depois acessar a aplicação admin e colocar seu usuário e senha, você poderá acessar o sistema de users e groups da aplicação padrão do django.

    http://127.0.0.1:8000/admin/

CRIANDO A APLICAÇÃO

Criarei uma aplicação com o nome core que será padrão para todos os módulos do sistema, as coisas mais gerais estrão nesta aplicação

    python manage.py startapp core

Foi criado um novo diretório chamado core com os seguites arquivos e diretório:

 - /migratios -> Onde ficará as migrations
 - __init__.py - arquivo que informa que este dir e python
 - admin.py - registrar a aplicação dentro do nosso admin
 - apps.py - definiremos nossa app
 - models.py - definiremos nossas models
 - tests.py - usado para testes
 - views.py - definiremos nossas views

Registrando a aplicação no django

Para registrar a app criada, basta adicioná-la em INSTALLED_APPS no arquivo settings.py:
Mais antes movereio diretório core para dentro de simplemooc para fazer referência a ele.
Neste caso faz referência ao meu projeto

    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'simplemooc.core',
    ]

CRIANDO URL

Basta importar sua função view a chamá-la na url conforme o exemplo home abaixo

    from django.contrib import admin
    from django.urls import path
    from simplemooc.core.views import home

    urlpatterns = [
        path('', home, name='home'),
        path('admin/', admin.site.urls),
    ]

OBS: que fiz referência ao local da minha view w importei o objeto home dela

    from simplemooc.core.views import home

A minha view ficou com a seguinte função

    from django.shortcuts import render
    from django.http import HttpResponse

    def home(request):
        return HttpResponse('Hello World')

OBS: importei HttpResponse para poder retornar uma mensagem a página web

    return HttpResponse('Hello World')

INTRODUÇÃO AOS TEMPLATES

O que são templates?

 - Arquivois de textos com algumas marcações especiais.
 - Servem para gerar texto dinâmicamente, normalmente html.
 - Contém variáveis que são atribuídas por seu valor, tags que irão controlar o fluxo da apresentação e filtros que irão manipular o resultado da avaliação das variáveis.

 Exemplo de templates presente na documentação oficial https://docs.djangoproject.com/en/3.0/ref/templates/language/#variables

    <!DOCTYPE html>
    <html lang="en">
        <head>
            <link rel="stylesheet" href="style.css">
            <title>{% block title %}My amazing site{% endblock %}</title>
        </head>

        <body>
            <div id="sidebar">
                {% block sidebar %}
                <ul>
                    <li><a href="/">Home</a></li>
                    <li><a href="/blog/">Blog</a></li>
                </ul>
                {% endblock %}
            </div>

            <div id="content">
                {% block content %}{% endblock %}
            </div>
        </body>
    </html>

OBS: A ideia do django é que você separa sua vizualização do código, por isto temos os templates.

MTV - Model Templates View - esta é a base do django.

OBS: Os TEMPLATES é a forma como os dados serão visto e a VIEWS é como os dados serão vistos.

Váriáveis do Template

Terão seu valor substituído na saída do template e seu nome deve ter aspas, caracteres alfanuméricos e o underscore "_", com a seguinte sitaxe

    {{ nome_variavel }}

Variáveis pode ser também um objeto complexo, um dicionario, uma lista, e para acessar um atributos deste objeto basta colocar o "."(ponto).

    - {{ meu_dicionario.chave }}
    - {{ meu_objeto.atributo }}
    - {{ meu_objeto.metodo }}
    - {{ minha_lista.0 }}

Tags do Tamplate https://docs.djangoproject.com/en/3.0/ref/templates/builtins/

 - Fazem controle como pro exemplo IFs.
 - São usados para lógicas mais complexas.
 - Podem retornar um valor a serem preenchidos no templates, controlar fluxos de saída, carregar informaçãos adicionais
 - Sintaxe:

    - {% tag %} conteúdo {% endtag %}
    - {% tag param1 param2 %} conteúdo {% endtag %}
    - {% tag %} conteúdo {% endtag %}
    - {% tag param1 param2 %}

 - Exemplo:

    {% if athlete_list|length > 1 %}
        Team: {% for athlete in athlete_list %} ... {% endfor %}
    {% else %}
        Athlete: {{ athlete_list.0.name }}
    {% endif %}

Filtros no template

 - São usados para formatar o valor de uma variável
 - Sintaxe:
  
    - {{ variavel|lower }}
    - {{ variavel|default:"padrão"}}

 - Podem ser aninhados
    
    - {{ variavel|random|lower }}

PRIMEIRO TEMPLATE

Com seu ambiente virtual ativo acesso o dir /simplemooc do seu projeto e digite o seguinte comando:

    python manage.py shell

É basicamente executar o shell do python, porem com o ambiente django esta carregado com suas funções e variáveis...

Execute o seguinte comando com o shell em execução

    from django.template import Template, Context    

Context - é o conjunto de variáveis disponíveis para um determinado Template

Criando o template

    template = Template("Bem vindo: {{ usuario }}")

Criando o contexto

    context = Context({"usuario":"Davi Bernardo"})

Redenrizar o Contexto com o Template

    print(template.render(context))

Obtem o seguinte retorno

    Bem vindo: Davi Bernardo

Crinado um template com o filtro lower (deixar tudo minúsculo)

    template = Template("Bem vindo: {{ usuario|lower }}")

    print(template.render(context))

    Bem vindo: davi bernardo

OBS: os tmplas serão criados em paginas .html, pois ficarão mais intuitivos.

Fechado o shell

    exit()

OBS: O django é baseado em MTV 

 - MODEL - Persistência dos dados
 - TEMPLATES - Molde como os dados serão visualizados
 - VIEWS - Quê dados serão visualizados

CRIANDO O TEMPLATE

É necessário criar um deiretório chamado templates dentro da nossa APP CORE, pois dentro dele ficará todos nosso templates.

    /core/templates

Por padrão é necessário cada app tenha ums diretório chamado de template

Criando a home em nosso diretório templates

    /core/templates
                home.html


Template home básico

    <!DOCTYPE html>
    <html lang="br">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>Simple MOOC</title>
        </head>
        <body>
            Usuário: {{ usuario }}
        </body>
    </html>

View chamando o Template home básico usando o render

    from django.shortcuts import render
    from django.http import HttpResponse

    def home(request):
        return render(request, 'home.html', {'usuario': 'Fulano de Tal'})

TEMPLATE BASE

PURE CSS

Usaremos o pure css ao invés de bootstrap do TWITTER, apenas pra informar que existem outros framewoks html, este por exemplo e matido pela YAHOO https://purecss.io/

Implementando o layout do pure css ao meu arquivo template home.html

OBS:  dentro de cada App é necessário criar um diretório chamadno static que ficará o css, js

    /core/static/css/arquivos.css

no 

É necessário declarar o novo módulo css com o seguinte comando na cabeçalho da página

    {% load static %}

E com a seguinte chamanda css

    <link rel="stylesheet" href="{% static 'css/styles.css' %}" />

Exemplo final da template home

    <!doctype html>
    {% load static %}
    <html lang="en">
        <head>
            <meta charset="utf-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <meta name="description" content="Simple MOOC - Uma simples plataforma de ensino a distância" />
            <title>Simple MOOC</title>
            <link rel="stylesheet" href="http://yui.yahooapis.com/pure/0.3.0/pure-min.css">
            <link rel="stylesheet" href="{% static 'css/styles.css' %}" />
        </head>
        <body>
            conteudo
        </body>
    </html>

PÁGINA DE CONTATO

Basta criar uma nova view, depois criar o arquivo contact.html e rotear o mesmo conforme os scripts abaixo:

View contato

    def contact(request):
        return render(request, 'contact.html')

Templates contato

    contact.html

Url contato

    from simplemooc.core.views import home, contact

HERANÇA DE TEMPLATES

É interessante os templates herdarem parte de um template master. Sendo uma base padrão que os demais evitando repetição em códigos.

Crie um templates base.html e nele coloquei todo o código que ser repete, ex: cabeçalho e rodapé.
Criei a seguinte bloco dentro da class content que serirá como placeholder para os demais templates

    {% block content %} {% endblock %}

Nos templates que herdarão a base.html basta colocar o seguinte código no início da página

    {% extends "base.html" %}
    {% block content %}
        .......
        contéudo da página
        .......
    {% endblock content %}

Template base.html

    <!doctype html>
    {% load static %}

    <html lang="en">
        <head>
            <meta charset="utf-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <meta name="description" content="Simple MOOC - Uma simples plataforma de ensino a distância" />
            <title>Simple MOOC</title>
            <link rel="stylesheet" href="http://yui.yahooapis.com/pure/0.3.0/pure-min.css">
            <link rel="stylesheet" href="{% static 'css/styles.css' %}" />
        </head>
        <body>
            <div class="header">
                <div class="pure-menu pure-menu-open pure-menu-fixed pure-menu-horizontal">
                    <a class="pure-menu-heading" href="{% url 'home' %}">SIMPLE MOOC</a>
                    <ul>
                        <li class="pure-menu-selected"><a href="{% url 'home' %}">Início</a></li>
                        <li><a href="#">Cursos</a></li>
                        <li><a href="{% url 'contact' %}">Contato</a></li>
                    </ul>
                </div>
            </div>
            <div class="content">
                {% block content %} 
                {% endblock %}
                <div class="footer">
                    Simple MOOC - Uma simples plataforma de ensino a distância
                </div>
            </div>
            <script src="http://yui.yahooapis.com/3.12.0/build/yui/yui-min.js"></script>
        </body>
    </html>

Demais templates, neste cado contac.html

    {% extends "base.html" %}
        {% block content %}
            <div class="pure-g-r content-ribbon">
                <div class="pure-u-1">
                    <h1>Fale conosco</h1>
                    <p>Você pode entrar em contato conosco tanto por e-mail como pelas redes sociais, abaixo seguem os links para contato:</p>
                    <h4>Links</h4>
                    <ul>
                        <li>E-mail: <a href="mailto:contato@simplemooc.org">contato@simplemooc.org</a></li>
                        <li>Twitter: <a href="https://twitter.com/simplemooc">@simplemooc</a></li>
                    </ul>
                </div>
            </div>
        {% endblock %}

OBS: Neste conceito diminui bastante a repetição de uma página

