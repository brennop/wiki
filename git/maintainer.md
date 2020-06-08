# Guia do Mantenedor

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

> Ferramenta para gerar projeto, como o `reate-react-app`
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
config: remove o link hardcoded da api
estilo: aumenta o tamanho da navbar
refactor: altera o uso de contexto no app
```

- Incluir o link do issue tracker no footer

> Usar emojis no lugar de palavras para o tipo pode salvar
> alguns caracteres

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

> Use o [plugin do
> git](https://github.com/git/git/blob/master/contrib/completion/git-completion.bash)
> para bash/zsh para melhorar o tab-completion dentro do
> git.

### Mensagens de Request

## Revisando Código

### Não tenha medo de dizer não
