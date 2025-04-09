# Configurações Iniciais no Linux

Comandos para configurar um ambiente de trabalho no Linux.

## Instalar WSL2
Use o PowerShell como administrador para executar os comandos abaixo.
### Comando para Instalar WSL2

```powershell
wsl --install
```
### Em caso de problemas tente fazer a instalação manual do WSL2

- #### Etapa 1 – Habilitar o Subsistema do Windows para Linux
```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```
- #### Etapa 2 – Verificar os requisitos para executar o WSL 2
Para atualizar para o WSL 2, você precisa estar executando o Windows 10.

Em sistemas x64: versão 1903 ou posterior, com o Build 18362.1049 ou posterior.
Em sistemas ARM64: versão 2004 ou posterior, com o build 19041 ou posterior.
ou Windows 11.

Para verificar a sua versão e o número de build, selecione a tecla do logotipo do Windows + R, digite winver e selecione OK.

- #### Etapa 3 – Habilitar o recurso de Máquina Virtual
```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

- #### Etapa 4 – Baixar o pacote de atualização do kernel do Linux
O pacote de atualização do kernel do Linux instala a versão mais recente do kernel do Linux WSL 2 para executar o WSL dentro da imagem do sistema operacional Windows. (Para executar o WSL da Microsoft Store, com atualizações mais frequentes, use wsl.exe --install ou wsl.exe --update).
  1. Baixar o pacote mais recente:
  [Pacote de atualização do kernel do Linux do WSL2 para computadores x64](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

  2. Execute o pacote de atualização baixado na etapa anterior. (Clique duas vezes para executar. Você receberá uma solicitação para fornecer permissões elevadas; selecione 'sim' para aprovar essa instalação.)

- #### Etapa 5 – Definir o WSL 2 como a sua versão padrão

```powershell
wsl --set-default-version 2
```

- #### Etapa 6 – Instalar a distribuição do Linux de sua escolha

Abra a Microsoft Store e escolha sua distribuição do Linux favorita.

## Instalar Pyenv

### Atualizar as listas de pacotes

Antes de tudo, atualize as listas de pacotes:

```bash
sudo apt update
sudo apt upgrade -y
```

### 1. Instalar pacotes essenciais para desenvolvimento

Rode o seguinte comando para instalar alguns pacotes necessários:

```bash
sudo apt-get install -y build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm gettext libncurses5-dev tk-dev tcl-dev blt-dev libgdbm-dev git python3-dev aria2 libnss3-tools python3-venv liblzma-dev libpq-dev
```


Explicação dos pacotes principais:

- build-essential: Ferramentas de compilação como gcc e make.

- libssl-dev: Bibliotecas para suporte a SSL.

- zlib1g-dev: Biblioteca de compressão de dados.

- libbz2-dev: Biblioteca de compressão Bzip2.

- libreadline-dev: Biblioteca para histórico e edição de linha de comando.

- libsqlite3-dev: Biblioteca para o SQLite.

- wget/curl: Ferramentas para download de arquivos pela internet.

- llvm: Ferramenta para otimização e compilação de código.

- gettext: Suporte para internacionalização.

- libncurses5-dev: Biblioteca para interfaces de terminal.

- tk-dev/tcl-dev/blt-dev: Bibliotecas para GUIs baseadas em Tk.

- libgdbm-dev: Biblioteca GNU dbm.

- git: Controle de versão.

- python3-dev: Cabeçalhos de desenvolvimento para Python 3.

- aria2: Ferramenta para downloads multi-protocolos.

- libnss3-tools: Ferramentas de suporte para segurança de rede.

- python3-venv: Suporte para ambientes virtuais em Python 3.

- liblzma-dev: Biblioteca de compressão LZMA.

- libpq-dev: Bibliotecas de desenvolvimento para PostgreSQL.


### 2. Instalar o Pyenv

O Pyenv é uma ferramenta para gerenciar diferentes versões do Python em um mesmo sistema. Ele permite instalar, alternar e manter múltiplas versões do Python, tornando o desenvolvimento mais flexível e compatível com diferentes projetos.

Use o seguinte comando para instalar o Pyenv:

```bash
curl https://pyenv.run | bash
```

### 3. Configurar o bashrc para ativar o Pyenv automaticamente

a. Copie as linhas que aparecerão ao final da instalação anterior:

```bash
export PATH="~/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
```

b. Edite o arquivo `.bashrc` para adicionar essas linhas ao final:

```bash
nano ~/.bashrc
```

c. Feche e reabra o terminal para aplicar as mudanças (ou execute `source ~/.bashrc` para aplicar as mudanças sem fechar o terminal).

## Instalar o Git

### Verificar versão e instalar o Git

Verifique se o Git está instalado:

```bash
git --version
```

Caso não esteja instalado, use o comando:

```bash
sudo apt install git
```

### Configurar usuário e e-mail

Verifique se existe um usuário configurado:

```bash
cat ~/.gitconfig
```

Ou:

```bash
git config --list
```

Caso precise configurar um novo usuário:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu.email@exemplo.com"
```

Explicação:

- O uso de `--global` aplica essas configurações a todos os repositórios no sistema do usuário.

- Sem o `--global`, as configurações se aplicam apenas ao repositório atual.

Se houver algum erro e precisar deletar o arquivo de configuração:

```bash
rm ~/.gitconfig
```

## Configurar Repositório para Trabalhar com Fork de uma Organização

### 1. Fazer Fork da Organização

Faça o fork do repositório da organização para o seu GitHub pessoal. Verifique quais *branches* existem e se é necessário trazer todas ou apenas a *branch* principal.

### 2. Clonar o Repositório para o Ambiente Local

Clone o repositório do seu GitHub:

```bash
git clone <URL_DO_REPOSITORIO>
```

Para verificar quais *branches* estão disponíveis (tag `-a` mostra tanto locais como remotas):

```bash
git branch -a
```

### 3. Configurar o Repositório Upstream

Adicione o repositório da organização como `upstream`:

```bash
git remote add upstream <URL_DO_REPOSITORIO_ORIGINAL>
```

Verifique se deu certo:

```bash
git remote -v
```

Se precisar mudar a URL do *remote*:

```bash
git remote set-url origin <NOVA_URL_DO_REPOSITORIO>
```

### 4. Atualizar o Repositório Local com a Organização

a. Traga as atualizações diretamente do repositório da organização:

```bash
git fetch upstream
```

b. Atualize sua *branch* local (faça para cada *branch* que precisar):

- Mude para a *branch* que deseja atualizar:

```bash
git switch <BRANCH>
```
Ou `checkout` para compatibilidade com versões mais antigas do Git.
```bash
git checkout <BRANCH>
```

- Traga as mudanças do *upstream*:
A opção `--rebase` evita merges desnecessários, mantendo um histórico linear e mais limpo. Diferente do `merge`, que cria um commit de merge, o `rebase` aplica suas mudanças sobre a base mais recente, tornando o histórico mais fácil de seguir.
```bash
git pull upstream <BRANCH> --rebase 
```

### 5. Atualizar o Repositório Remoto Pessoal

Atualize seu repositório remoto pessoal (*origin*):
Use este comando para empurrar uma branch nova para o repositório remoto pela primeira vez.
```bash
git push -u origin <BRANCH>
```
Se a branch já foi empurrada anteriormente, apenas `push` é suficiente, tornando o comando mais eficiente:
```
git push
```

### 6. Configurar Repositório Remoto Padrão

Configure seu *origin* como repositório padrão para uso dos comandos `checkout` ou `switch`:

```bash
git config checkout.defaultRemote origin
```

Defina o comportamento padrão para o comando `git push`, simplificando o envio de alterações para o repositório remoto padrão. Isso garante que apenas a branch atual será empurrada para o repositório remoto correspondente:

```bash
git config --global push.default simple
```

## Comandos importantes

- Descartar mudanças não enviadas para *área de staging* (ainda não usou `git add`):
  ```bash
  git restore <ARQUIVO>
  ```
  Pode usar também `git checkout -- <ARQUIVO>` para compatibilidade com versões mais antigas.
  
  Ou, se quiser descartar todas as mudanças não salvas de uma vez:
  ```bash
  git restore .
  ```
  Pode usar também `git checkout -- .` para compatibilidade com versões mais antigas.
  
- Descartar mudanças já enviadas para *área de staging*:
  ```bash
  git restore --staged <ARQUIVO>
  ```
  
  Ou, se quiser remover todos os arquivos da área de staging de uma vez:
  ```bash
  git restore --staged .
  ```
  Alternativas: `git reset <ARQUIVO>`, ou `git reset .`. Pode retirar da *área de staging* e ao mesmo tempo descartar as mudançãs, voltando para o estágio do ultimo *commit* com `git reset --hard`.

**Muito cuidado** ao usar comandos que voltam ao estado do último *commit*. Não é possivel retornar essas ações.

- Adicionar multiplos arquivos, mas não todos, à *staging*:
  - Adicionar arquivos individualmente:
    ```bash
    git add <ARQUIVO1> <ARQUIVO2>
    ```
  - Adicionar Arquivos em um Diretório Específico:
    ```bash
    git add <PATH/DO/DIRETORIO/>
    ```
  - Adicionar Arquivos com uma Extensão Específica:
    ```bash
    git add *.<EXTENSAO>
    ```
  
## Exemplo de Fluxo de Trabalho

Este fluxo pressupõe que todas as configurações locais e de acesso ao repositório já foram realizadas. Este é apenas um exemplo de fluxo de trabalho e pode precisar ser adaptado de acordo com as regras e práticas específicas da organização.

1. **Escolher uma Issue**:

   - Identifique a *issue* a ser trabalhada na organização, criando uma nova ou verificando uma existente. Exemplo: `#20`.

2. **Sincronizar com o Upstream**:

   - Certifique-se de que seu repositório local está atualizado com as últimas mudanças do repositório principal (*upstream*):
     ```bash
     git pull upstream <BRANCH> --rebase
     ```

3. **Sincronizar com o Origin**:

   - Sincronize seu repositório pessoal (*origin*):
     ```bash
     git push origin <BRANCH>
     ```

4. **Criar uma Branch para a Tarefa**:

   - Crie uma *branch* para a tarefa relacionada à *issue* a ser trabalhada e mude para a nova branch:
     ```bash
     git checkout -b <NOME_DA_BRANCH>
     ```
     Posso usar `git branch <NOME_DA_BRANDH>` para criar uma nova *branch*, mas vou ter que usar `git switch` ou `git checkout` para mudar para a nova *branch*.

5. **Realizar Commits**:

   - Faça *commits* no progresso do trabalho, utilizando a expressão `closes #20` para fechar a *issue* ao concluir:
     ```bash
     git commit -m "Descrição do trabalho - closes #20"
     ```

6. **Enviar a Branch para o Repositório Remoto**:

   - Empurre a *branch* de trabalho para o seu repositório remoto (apenas necessário se a *branch* ainda não existir no remoto):
     ```bash
     git push -u origin nome-da-branch
     ```
     ou:
     ```
     git push
     ```

7. **Criar Pull Request no GitHub**:

   - No GitHub, crie o *pull request* da sua *branch* de trabalho para a organização.

8. **Limpeza de Branches**:

   - Após o *pull request* ser aceito, delete a *branch* do remoto e do local:
     ```bash
     git push origin --delete nome-da-branch
     git branch -d nome-da-branch
     ```
     Se a branch local não foi completamente mesclada e precisa ser forçada a ser removida, use `git branch -D nome-da-branch`, mas use com cautela, pois isso pode resultar em perda de trabalho não integrado.
     ```bash
     git branch -D <nome-da-branch>
     ```

---

Este fluxo ajuda a manter o repositório organizado e facilita o rastreamento de alterações e resoluções de *issues*.

