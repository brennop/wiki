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

JSX nos permite avaliar expressões JavaScript no meio das nossas expressões
JSX
