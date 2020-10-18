# JSX

> Durante anos tentamos separar lógica de negócio de interface de usuário. Aí
> chegou o React e mudou tudo. - Comentário aleatório no Hacker News

JSX é uma extensão de sintaxe para o JavaScript. Ela nos permite descrever a
nossa interface (UI) no meio do nosso JavaScript.

```javascript
const elemento = </h1>Olá Mundo</h1> // pera, isso não é ilegal? 🤔
```

Tudo que está entre as tags `<h1>` será interpretado como texto. Mas e se
quisermos usar nossas variáveis JavaScript para compor nossa interface?

## Expressões

E como fazemos pra misturar nossa lógica com a nossa marcação?

```javascript
const quatro = 4;
const elemento = <p>2 + 2 é {quatro}</p>;
```

Usando chaves, é possível envolver qualquer [expressão
JavaScript](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Guide/Expressions_and_Operators)
válida com JSX.

## Atributos

É possível associar atributos aos elementos de marcação. Se quisermos associar
um atributo a uma tag, basta escrever o nome do atributo e seu valor, da
seguinte forma.

```javascript
const link = <a href="https://pt-br.reactjs.org">Documentação do React</a>;
```

Além de string literais, também podemos usar expressões JavaScript como valor
para os nossos atributos. Basta envolver o atribuição do valor com chaves, como
vimos em [Expressões](#expressões).

```javascript
const avatar = <img src={user.avatarUrl} />;
```

> Apesar de representarem elementos reais do DOM, o React adotou o padrão
> camelCase para representar os atributos. Isso quer dizer que atributos como
> `tabindex` não são suportados, e devem ser substituídos pelo sua versão em
> camelCase: `tabIndex`.
