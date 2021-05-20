# Ambiente de Desenvolvimento CJR

Essas são as ferramentas que usamos na CJR para desenvolver e garantir a qualidade dos projetos.

Enquanto disponibilizamos a maior parte das instalações para Windows, recomendamos que usem um sitema baseado em Unix, como o Linux ou o macOS, pois têm melhor suporte a essas ferramentas. Como a maior parte dos membros usam sistemas como esses, vai ser mais fácil obter ajuda.

Se você nunca usou Linux antes, recomendamos que comece pelo o [Ubuntu](https://ubuntu.com/download/desktop)

## Git

Git é um sistema de controle de versões distribuído, que usamos para gerenciar o desenvolvimento de software nos nossos projetos. Ver [Git](git/)

### Instalação

#### Linux

Git está disponível na maioria dos gerenciadores de pacotes. No Ubuntu/Debian por exemplo, basta utilizar os seguintes comandos:

```bash
sudo apt update
sudo apt install git-all
```

#### Windows

A maneira mais fácil é baixando e instalando os binários disponíveis no site oficial do git:

https://git-scm.com/downloads

Se o gerenciador de pacotes `chocolatey` estiver disponível, basta utilizar o comando:

```bash
choco install git
```

#### macOS

Primeiro, é útil verificar se o Git já não está presente não sua instalação

```
git --version
```

Se não, instale os binários fornecidos no [site oficial](https://git-scm.com/downloads) ou obtenha o Xcode Command Line Tools.

Se o gerenciador de pacotes `homebrew` estiver disponível, basta utilizar o comando:

```bash
brew install git
```

### Configuração

Antes de começar a utilizar o Git é necessário configurar um nome e e-mail para identificar seus commits. Digite esses comandos no terminal do seu sistema ou no interface Git Bash fornecida pelo instalador no Windows:

```bash
git config --global user.name "Nome Sobrenome"
git config --global user.email "email@dominio.com"
```

## Node

[Node.js](https://nodejs.org) é um ambiente de tempo de execução para JavaScript com um rico ecossistema de bibliotecas.

### Linux

Para Ubuntu/Debian:

```bash
curl -sL https://deb.nodesource.com/setup_13.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Agora vamos instalar o `yarn`, gerenciador de pacotes do Node desenvolvido pelo Facebook. No Ubuntu/Debian:

```bash
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update && sudo apt-get install yarn
```

### Windows

Vá para o site oficial do [Node.js](https://nodejs.org) e faça o download da versão mais recente e siga os passos da instalação.

Para instalar o `yarn`, basta [baixar os binários](https://classic.yarnpkg.com/pt-BR/docs/install/#windows-stable) e seguir os passos da instalação.

Se o gerenciador de pacotes `chocolatey` estivar disponível basta utilizar os comandos:

```bash
choco install nodejs
choco install yarn
```

### macOS

Vá para o site oficial do [Node.js](https://nodejs.org) e faça o download da versão mais recente e siga os passos da instalação.

Para instalar o `yarn`, um método recomendado é utilizar o script de instalação fornecido:

```bash
curl -o- -L https://yarnpkg.com/install.sh | bash
```

Se o gerenciador de pacotes `homebrew` estivar disponível basta utilizar os comandos:

```bash
brew install node
brew install yarn
```

## Ruby

Para a instalação do Ruby e do Rails, vamos utilizar o [Ruby Version Manager](https://rvm.io).

> Não recomendamos a instalação do Ruby por outros meios

### Instalação

No Ubuntu, é necessário instalar algumas ferramentas primeiro.

```bash
sudo apt update
sudo apt install curl gnupg2 build-essential
```

Prossiga com a instalação do RVM

```bash
gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
\curl -sSL https://get.rvm.io | bash -s stable
```

Reabra o terminal para que o shell possa iniciar o rvm corretamente e prossiga com a instalação do Ruby na versão correta

```bash
rvm install 2.6.0
rvm --default use 2.6.0
```

> A instalação para macOS segue passos semelhantes

> No momento só é possível instalar o RVM no Windows utilizando WSL ou Cygwin.
> A instalação para WSL segue os mesmos passos dessa seção.
> Se não quiser utilizar o WSL, também é possível instalar o Ruby manualmente no
> Windows baixando um instalador no https://rubyinstaller.org

### Configuração no `gnome-terminal`

Se estiver usando o terminal padrão do Ubuntu, é necessário fazer algumas alterações para garantir que o RVM funcione corretamente.

Na barra superior vá em Edit > Preferences. Isso deve abrir uma janela com configurações do seu perfil. Vá na aba "Command" e selecione a opção "Run command as login shell".

![Configuração](https://i.imgur.com/C6Xko25.png)

https://rvm.io/integration/gnome-terminal

### Gems

Utilizaremos o Gem, o gerenciador de pacotes do Ruby, para instalar alguns pacotes (gems) que serão necessários para o desenvolvimento.

```bash
gem install bundler
gem install rails
```

> Rails requer um runtime de JavaScript para rodar seu Asset Pipeline. Se não tem certeza de que um
> está instalado, siga os passos de instalação do [Node](#node)

## PostgreSQL

O PostgreSQL é um sistema de bancos de dados relacional, open source e mantido pela comunidade.

### Instalação

#### Linux

Verifique a disponibilidade do PostgreSQL na sua distribuição. No Ubuntu/Debian, vamos instalar da seguinte forma:

```bash
sudo apt update
sudo apt install postgresql postgresql-contrib libpq-dev
```

#### macOS

Escolha uma das opções de instalação disponibilizadas [aqui](https://www.postgresql.org/download/macosx/).

#### Windows

Faça o download de um dos binários fornecidos pelo EnterpiseDB fornecidos [aqui](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads).

### Configuração

Vamos entrar no console interativo do PostgreSQL para criar um usuário privilegiado. Entre no terminal como o usuário do `postgres`:

```bash
sudo -i -u postgres
```

Inicie o terminal do PostgreSQL:

```bash
psql
```

Crie um usuário e garanta que tenha privilégios elevados:

```sql
CREATE USER nome WITH PASSWORD 'senha';
ALTER USER nome WITH SUPERUSER;
```

> Altere os campos 'nome' e 'senha' para valores que desejar

> Não esqueça o `;` no final dos comandos!

Para verificar que o usuário foi criado digite o comando `\du`. Para sair do terminal do PostgreSQL digite `\q` ou Ctrl+D.

## zsh

O Zsh é um shell que oferece diversas vantagens sobre shells padrão, como uma melhor tab-completion e frameworks úteis.

### Instalação

#### Linux

Zsh está disponível em diversos gerenciadores de pacotes. No Ubuntu/Debian, a instalação é direta:

```bash
sudo apt update
sudo apt install zsh
```

#### macOS

Podemos usar o `homebrew` para instalar o `zsh`, se estiver disponível:

```bash
brew install zsh
```

### oh-my-zsh

Oh My Zsh é um framework para o `zsh` mantido pela comunidade, oferecendo plugins e opções de customização do shell. Para instala, vamos usar o script de instalação disponibilizado pelo [site oficial](https://ohmyz.sh/):

```bash
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

Durante a instalação você será solicitado a tornar o `zsh` seu shell padrão. Digite enter para confirmar.

### Configurando um shell padrão

Se você não conseguir configurar o `zsh` como o seu shell padrão durante a instalação do Oh My Zsh, pode usar o comando `chsh` para definir um shell.

```bash
chsh -s /usr/bin/zsh
```

## Editor de Texto

### Visual Studio Code

O editor preferido entre os membros da CJR. Desenvolvido pela Microsoft, open-source e disponível em todas as plataformas. Esse editor conta com um grande ecossistema de plugins que complementam a usabilidade do editor, tornando a sua vida de desenvolvedor mais fácil.
https://code.visualstudio.com/

### RubyMine e WebStorm

IDEs fornecidas pela JetBrains, são bem completas e cheias de features. Você pode ter acesso às versões completas usando o seu e-mail da UnB, já que são ferramentas pagas por padrão.
https://www.jetbrains.com/webstorm/
https://www.jetbrains.com/ruby/

### Outras Opções

- [Atom](https://atom.io/): editor de texto para desenvolvimento mantido pelo GitHub. Bem semelhante ao VS Code, mas um pouco mais pesado.
- [Vim](https://www.vim.org/): Literalmente o melhor editor dessa lista. Os fiéis seguidores da Igreja do Brennoia têm a bênção para codar com esse editor.
