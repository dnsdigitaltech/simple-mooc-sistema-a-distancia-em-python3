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