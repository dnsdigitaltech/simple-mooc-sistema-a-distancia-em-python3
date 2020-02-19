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
 