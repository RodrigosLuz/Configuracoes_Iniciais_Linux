# Configuracoes-Iniciais-Linux
Comandos para configurar ambiente de trabalho no linux

## Instalar Pyenv

Antes vamos atualizar as listas de pacotes:
```
sudo apt update
```

### 1 - Primeiro rodar no terminal esse comando para instalar alguns pacotes importantes para desenvolvimento:

```
sudo apt-get install -y build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm gettext libncurses5-dev tk-dev tcl-dev blt-dev libgdbm-dev git python3-dev aria2 vim libnss3-tools python3-venv liblzma-dev libpq-dev
```

### 2 - Digitar o segunte comando para instalar o pyenv:

```
curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash
```

### 3 - Adicionar linhas no bashrc para ativar o pyenv automaticamente.

a - Copiar as 2 linhas que aparecem ao fim da instalação anterior:
```
export PATH="~/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
```
b - Digitar o comando para entrar no bashrc:
```
vim .bashrc
```
c - Colar as linhas no final do arquivo: (Usar tecla insert > colar > esc)

d - Salvar e sair digitando: ```:x```

e - fechar e abrir o terminal novamente.

## Instalar GIT

Verificar se existe uma versão do GIT já instalada: `git --version`

Instalando GIT: `sudo apt install git`

Verificando se existe um usuário configurado: `cat ~/.gitconfig` ou `git config --list`

Configurando um Usuário: `git config --global user.name 'digite um nome'`

Configurando um email: `git config --global user.email 'digite um email'`

Se o usuário ou email estiver errado (deletar o arquivo): `rm ~/.gitconfig`
