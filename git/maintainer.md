# Guia do Mantenedor

![](https://imgs.xkcd.com/comics/git.png)

## Das responsibilidades

- Manter a estrutura do projeto organizada
- Manter o histórico do projeto consiso
- Garantir uso dos padrões acordados
- Garantir que o código de qualidade seja adicionado ao
  projeto

## O repositório remoto

O repositório remoto é a fonte centralizado do seu código,
e deve ser a fonte da verdade.

### Iniciando um repositório git

```
git init
```

> Ferramentas para gerar projeto, como o `reate-react-app`
> e o `rails new` fazem esse passo automaticamente

### Adicionando a branch de desenvolvimento

```
git branch develop
```

### Criando o repositório remoto

Crie um repositório privado sem README no GitLab/GitHub.

### Subindo seu projeto para o repositório remoto

```
git remote add origin url_do_projeto
git push -u origin master
```

### Adicionando os desenvolvedores

Adicione seus desenvolvedores na aba `Members` do GitLab, ou
na aba `Manage Access`, dentro de Settings no GitHub.

## Definindo Padrões

Padrões dentro de uma equipe de desenvolvimento podem
ajudar a garantir que o projeto permaneça organizado
e sustentável.

> Lembre-se que o seu projeto pode ser passado para um novo
> time de desenvolvedores no futuro. Ninguém quer lidar com um
> projeto bagunçado.

### Padrões de mensagem

Definir um padrão para as mensagens de commit torna mais
fácil identificar do que um determinado commit trata.
É sempre bom acordar com o time esses padrões para que
a história fique consistente.

Alguns padrões _convencionais_ de mensagens de commit:

- Limite o resumo/título à 50 caracteres
- Escreva o resumo/título no imperativo da segunda pessoa
- Limite as linhas do corpo a 72 caracteres
- Pule uma linha entre o resumo e o corpo

Alguns padrões adicionais:

- Começar a mensagem com o tipo das mudanças

```
feat: implementa a navbar
fix: corrige o bug navbar muito pequena
tarefa: remove o link hardcoded da api
estilo: aumenta o tamanho da navbar
refactor: altera o uso de contexto no app
```

- Incluir o link do issue tracker no footer

> Usar emojis no lugar de palavras para o tipo pode salvar
> alguns caracteres

#### Template de mensagem de commit

```
# <tipo>: (Se aplicado esse commit...) <resumo>

# Explique o porquê do commit (opicional)

# Deixe links para qualuer conteúdo relevante (artigos, ticket)

# --- Fim do Commit ---
# Tipo pode ser um de
#   feat
#   fix
#   tarefa
#   estilo
#   refactor
# --------
```

### Padrões de branches

Nomeação padronizada de branches pode ajudar o mantenedor
a identificar mais fácilmente o objetivo de uma branch.
Um padrão comum usado é:

```
{tipo}/{resumo}/{prefix}{id}
```

- tipo: um de uma lista pré-definida (feat, fix, test,
  etc...)
- resumo: 2-3 palavras que descrevem o tópico da branch,
  separados por traço
- id: identificador do issue tracker, se existir, aliado
  a um prefixo, pra ajudar o tab-completion

Esse formato pode ser alterado para corresponder com as
necessidades do time. Ex.: trocar o tipo pelo apelido do
desedesenvolvedor.

> Use o [plugin do git](https://github.com/git/git/blob/master/contrib/completion/git-completion.bash)
> para bash/zsh para melhorar o tab-completion dentro do
> git.

### Mensagens de Request

O GitHub e o GitLab permitem definir templates para seus
merge requests/pull requests. Para adicionar um, basta
seguir as instruções da plataforma específica.

- [GitLab](https://docs.gitlab.com/ee/user/project/description_templates.html#creating-merge-request-templates)
- [GitHub](https://help.github.com/en/github/building-a-strong-community/configuring-issue-templates-for-your-repository)

#### Exemplo de Template

```markdown
## Porque esse merge é necessário

Descreva com algumas palavras o motivo desse merge request.

## O que esse merge faz

- Implementa essa feature
- Melhora a implementação daquela interface
- Altera o estilo dessas componentes

## Card relacionado

link para o card no trello
```

## Revisando Código (Code Review)

O objetivo do code review é garantir o a qualidade da base
de códigos. Ambos GitLab e o GitHub oferecem ferramentas
para facilitar o code review.

### Por que fazer code review?

- Reduz a quantidades de bugs que são introduzidos na sua base de código.
- Melhora o seu modelo de como o projeto está estruturado.
- Cria a oportunidade de aprender coisas novas.

### Merge Request/Pull Request

Para submeter um código para revisão, um desenvolvedor deve
criar um novo MR/PR da sua branch de tópico para a branche
de desenvolvimento.

A partir daí, o mantenedor e os desenvolvedores podem
visualizar e revisar as modificações que o merge irá causar
na aba de mudanças no request.

### Aprovando mudanças (Merge)

Aprovar mudanças significa juntar uma branch de tópico à sua
branch de desenvolvimento. Para fazer isso, basta utilizar
a interface web do GitLab/GitHub, ou fazer localmente usando
a interface de comandos do git.

```sh
git fetch origin
git checkout -b feat origin/feat
git merge --no-ff feat
git push origin master
```

Usar a interface do git pode ser a única maneira de resolver
conflitos.

### Estratégias alternativas

#### Fast-forward

Omitir o argumento `--no-ff` permite que um fast-forward
aconteça, quando possível. Nesse caso, as mudanças da branch
fonte são aplicadas na branch destino sem gerar um merge
commit.

#### Squash

Usar o argumento `--squash`, ou selecionar a opção de Squash
nas interfaces web, permite que um squash seja feito. Nesse
caso, todos os commits de alteração da branch fonte são
juntados em um commit só, que será aplicado na branch de
destino.

#### Rebase

Usar o commando `rebase` do git no lugar de `merge` permite
que um rebase aconteça. Nesse caso, todas as modificações da
branch fonte são aplicadas uma a uma na branch destino. Essa
estratégia deve ser usada com cuidado, já que modificam
a história. Por esse motivo, um rebase requer um push
forçado, pra forçar a repositório remoto a aceitar uma
história diferente.

Conflitos podem ocorrer durante a aplicação de mudanças.
Nesse caso, deve-se corrigir os conflitos para continuar
o processor.

### Rejeitando mudanças

Algumas vezes mudanças de baixa qualidade, com código ruim
ou mal formatado podem aparecer. Nesses casos é importante
comunicar com o desenvolvedor que são necessárias alterações.

Se a requisição não chegar ao nível necessário de qualidade
do projeto, deve-se recusar a requisição.

### Dicas de Code-Review

- Seja educado nos feedbacks

> ❌ Esse código está errado
>
> ❌ Você deve fazer da seguinte forma

> ✅ Notei que esse efeito pode acontecer com o seu código
>
> ✅ O que você acha de fazer da seguinte forma

- Deixe comentários sobre o que os desenvolvedores fizeram bem para incentivar e aumentar a moral.
- Apresente possíveis soluções quando achar que pode haver um
  problema.

## Desfazendo Coisas

https://github.com/k88hudson/git-flight-rules

Git pode ser complicado às vezes, então é fácil se enganar
com algum comando e coisas inesperadas acontecerem. Pra sua
sorte, se algo foi commitado, você provavelmente não perdeu
seu trabalho.

### Push na master/develop

Se um desenvolvedor deu um push na master/develop
acidentalmente, é simples resolver.

```
git revert hash_do_commit
```

Isso vai gerar um novo commit desfazendo as mudanças do
commit. Se vários commits foram adicionados em sequência,
basta usar

```
git revert primeiro_commit^..ultimo_commit
```

Se você quer manter a história limpa, sem o commit
acidental, você pode resetar para o commit mais recente
antes do commit acidental

```
git reset --hard commit_bom
git push --force-with-lease
```

> Considere setar branches de master/develop como protegidas
> para prevenir que desenvolvedores façam push

### Desfazendo um merge/rebase

Antes de fazer operações perigosas como merge/rebase, o git
salva o ponteiro HEAD em uma variável chamada ORIG_HEAD, pra
ficar fácil recuperar o estado anterior do seu projeto.

```
git reset --hard ORIG_HEAD
```

Também é possível desfazer um merge que ocorreu nas
interfaces web. Visualizando o request que ocasionou
o merge, as interfaces web te dão a oportunidade de realizar
um `revert` para desfazer as modificações de forma segura.

## Hooks

O Git permite que você defina hooks, que são ações
disparadas toda vez que algo importante acontece, como
quando um commit é feito. Para facilitar o gerenciamento
desses hooks, é possível usar o [Husky](https://github.com/typicode/husky).

### Instalando o Husky

```bash
yarn add -D husky
```

> É importante estar em um projeto Node

### Instalando o lint-staged

O [lint-staged](https://github.com/okonet/lint-staged)
permite rodar comandos, como linters, nos arquivos que foram
adicionados a staging area.

```bash
yarn add -D lint-staged
```

### Configurando os hooks

Os hooks podem ser configurados no `package.json`.

```json
"husky": {
  "hooks": {
    "pre-commit": "lint-staged"
  }
},

"lint-staged": {
  "*.js": [
    "yarn test --findRelatedTests --watch=false --bail",
    "prettier --write",
    "git add"
  ]
}
```

> Exemplo: roda os testes do Jest e executa o prettier pra
> formatar o código
>
> Esses pacotes precisam estar instalados no projeto
