# Git

![https://external-preview.redd.it/bcwn6a94GHAUWWSRsbYYCq1b5mltVNicNXuh6ReuHqA.jpg?width=617&auto=webp&s=430823ec55d31ccac64956981353b8324d8adc29](https://external-preview.redd.it/bcwn6a94GHAUWWSRsbYYCq1b5mltVNicNXuh6ReuHqA.jpg?width=617&auto=webp&s=430823ec55d31ccac64956981353b8324d8adc29)

> As with many great things in life, Git began with a bit of creative destruction and fiery controversy.

Git é um sistema de controle de versionamento (VCS) criado por Linus Torvalds.

---

## Instalação

### Linux

Instale usando o gerenciador de pacotes da sua distribuição. Em distribuições baseados no Debian, use o `apt` para instalar.

`sudo apt install git`

### Windows

A versão oficial do git para Windows está disponível em [https://git-scm.com/download/win](https://git-scm.com/download/win). É só baixar o arquivo e seguir os passos de instalação.

### MacOS

Se o XCode já estiver instalado, o Git provavelmente também deve estar instalado. Para testar, abra um terminal e digite `git --version`

## Configuração

O básico que você presica para usar o git é adicionar um nome e um email:

    $ git config --global user.name  "John Doe"
    $ git config --global user.email "johndoe@example.com"

### Configurações adicionais

#### Mudar o editor principal

    git config --global core.editor "nano -w"

#### Salvar senha e usuário

    git config --global credential.helper store

## Termos

- **Working Tree**: estado atual do diretório de trabalho
- **Staging Área**: arquivos marcados para o próximo commit

## Uso

### Getting started

- Inicializar um repositório

  Em um diretório não-git, execute o comando `git init`

- Adicionar uma url remota

  git remote add rotulo url

- Modificar uma url remota

        git remote set-url rotulo nova_url

- Clonar um repositório existente

        git clone https://url.do.repositório

### Salvando mudanças

- Verificar o estado dos arquivos

  `git status`

  _Dica:_ use `git status -s` para uma saída **s**implificada.

- Adicionar arquivos modificados para serem salvos

  `git add *arquivo1* *arquivo2*`

- Commitando as mudanças

  `git commit`

  `git commit -m *mensagem*` para adicionar a mensagem diretamente ao comando

  `git commit -a` para adicionar automaticamente arquivos trackeados

- Corrigindo um commit

  `git commit --amend` recria o último commit com as novas modificações. Útil quando houve um erro na mensagem de commit ou se esqueceu de adicionar um arquivo.

  Não modifique commits de outras pessoas!

- Visualizando as mensagens de commit

  `git log`

  _Dica_: use `git log --oneline` para obter um commit por linha

### Revertendo mudanças

- Desfazendo um `git add`

  `git reset*arquivo`\* ou `git reset` para desfazer todos

- Desfazendo mudanças não salvas [*]

  `git reset --hard arquivo` ou `git checkout arquivo` para retornar arquivo para a versão do último commit

  `git reset --hard` ou `git checkout HEAD` para retornar toda a [working tree] para a versão do último commit

- Revertendo um arquivo para uma versão específica

  `git checkout*fonte arquivo`* ou `git restore *arquivo* --source *fonte\*`

  onde fonte pode ser um hash de uma commit, uma branch ou um shorthand do tipo HEAD~1

- Desfazendo um commit

  `git revert id_do_commit` cria um novo commit desfazendo as mudanças do commit especificado.

  Nota: se você quer apenas alterar o último commit que ainda não foi enviado para o repositório remoto, veja [Corrigindo um commit]

- Desfazendo um `git reset --hard commit`

  Git guarda alguns commits por cerca de um mês antes de serem coletados pelo GC. Para visualizar as modificações use `git reflog`

  Com o hash do commit ou um shorthand do tipo HEAD@{0}, use `git reset id_do_commit` para retornar ao commit.

## Como escrever uma mensagem de commit

[https://udacity.github.io/git-styleguide/index.html](https://udacity.github.io/git-styleguide/index.html)

[https://chris.beams.io/posts/git-commit/](https://chris.beams.io/posts/git-commit/)
