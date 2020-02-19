# simple-mooc-sistema-a-distancia-em-python3
O Simple MOOC visa simplificar o ensino a distância, provendo ferramentas objetivas e de fácil uso para cursos a distância. Em Python 3

ESTE SISTEMA TERÁ AS SEGUINTES FUNCIONALIDADES:

 - Sistema de aulas {criar, editar e remover as aulas organizadas por módulos e associadas há um curso com aulas do youtube, materias para download e quiz}
 - Fórum de dúvidas {fórum aberto simples e separado por categorias, o usuário precisará está logado, para poder responder estes tópicos}
 - Exercícios de submissão {local onde os alunos enviarão arquivos como solução depois que o professor criar o exercício, com validação verificando se o conteúdo do aluno bate com o conteúdo que o professor criou, gerando notas}
 - Sistema de avisos {mural simples de avisos onde o professor cria o aviso e todos alunos recebem este aviso, também criaremos uma opção de comentários, podenedo receber os avisos por email}
 - Sistema de contas (usuários) {O aluno deverá está logado para acessar o seu curso, editar seu perfil}

CONFIGURANDO e ATIVANDO O PYTHON PARA SEU AMBIENTE (SO)

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

Aparece 

    (venv) desenv01@desenv01-Vostro-3583:~/Documentos/django2x-com-python3x$ no início do seu terminal 
