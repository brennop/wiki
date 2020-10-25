> 🚧 Seção em construção

# JSX

> Por anos tentamos separar UI de lógica. Aí chegou o JSX e nos provou errados.
>
> _comentário aleatório no HN_

## Referências

- [Introduzindo JSX](https://pt-br.reactjs.org/docs/introducing-jsx.html)
- [Renderização Condicional](https://pt-br.reactjs.org/docs/conditional-rendering.html)
- [Listas e Chaves](https://pt-br.reactjs.org/docs/lists-and-keys.html)
- [**JSX detalhado**](https://pt-br.reactjs.org/docs/jsx-in-depth.html)

## Intrudução

JSX é uma extensão do JavaScript que nos permite descrever a nossa UI dentro dos
nossos componentes.

```jsx
const elemento = <h1>Olá Mundo!</h1>;
```

> Pera um pouco, isso é _ilegal_! 😠
>
> - trainee vendo isso pela primera vez

No nosso exemplo, `elemento` não é uma string, ou um objeto HTML (_ainda_).
Elemento é um... _elemento_ 😩. Um _elemento_ é um objeto especial do React, que
sonha um dia em se tornar um objeto do DOM. Igual você, que sonha um dia em se
tornar um Cejotinha. Mas pra isso precisa aprender isso aqui primeiro.

```jsx
console.log(elemento);
// deve mostar algo assim, provavelmente 😅
// {
//   '$$typeof': Symbol(react.element),
//   type: 'h1',
//   key: null,
//   ref: null,
//   props: { children: 'Olá Mundo' },
//   _owner: null,
//   _store: {}
// }
}
```

Baseado na saída do log, um _elemento_ é só um objeto com coisas que não sabemos
pra que serve.

Mas há algumas chaves nesse objeto que importam pra gente. Como podemos
observar, `type` tem o mesmo valor que a nossa tag: `h1`. E olha onde nosso `Olá Mundo`
foi parar: dentro da chave `props` como valor de `children`.

## Expressões

Não teria graça colocar essa sintaxe nova dentro do JavaScript se a gente não
pudesse, bem, usar JavaScript dentro dela. Felizmente, podemos inserir qualquer
[expressão
JavaScript](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Guide/Expressions_and_Operators)
válida dentro no JSX. Basta _compreendê-la com chaves_.

```jsx
const name = "Trainee";
const elemento = <h1>Olá {name}</h1>;
// vai virar <h1>Olá Trainee</h1> quando for _renderizado_
```

Exemplos de expressões válidas são `2 + 2`, `user.name` ou `new Date().toLocaleString()`. Blocos de comentários também são expressões válidas.
Podemos usar isso para escrevermos comentários no nosso JSX.

```jsx
const Component = () => {
  return (
    <div>
      <p>Eu vou aparecer</p>
      <p>{/*Eu não vou aparecer*/}</p>
    </div>
  );
};
```

Expressões que avaliam para um valor `booleano`, `null` ou `undefined` não são
renderizadas. Isso quer dizer quer as seguintes expressões são equivalentes.

```jsx
<div />

<div></div>

<div>{false}</div>

<div>{null}</div>

<div>{undefined}</div>

<div>{true}</div>
```

### Condicionais

Se quisermos escolher o que [renderizar](trainee.md#Renderização), podemos usar
declarações `if` para escolhermos o que retornar do nosso componente.

```jsx
const BemVindo = (props) => {
  if (props.isLoggedIn) {
    return <h1>Bem vindo de volta!</h1>;
  }
  return <h1>Por favor, faça o login</h1>;
};
```

Não podemos usar declarações `if` dentro do JSX. Isso porque declarações `if`
_não são expressões JavaScript_. Temos algumas formas de contornar essa
limitações com expressões condicionais válidas.

#### O Operador `&&`

Geralmente usamos o operador `&&` para representar o operação lógica _and_. Em
JavaScript, porém, podemos usar este operador como um [operador de curto
circuito](https://pt.wikipedia.org/wiki/Avalia%C3%A7%C3%A3o_de_curto-circuito).

```jsx
const BemVindo = (props) => {
  return <h1>Bem Vindo {props.visits > 1 && <span>novamente</span>}</h1>;
};
```

No exemplo acima, `<span>novamente</span` só será avaliado se `props.visits` for
maior que 1. Lembre-se que isso é uma propriedade do JavaScript e não do React.

#### O operador ternário

Em breve...

> 💡 Para entender mais sobre renderização condicional, veja o [artigo
> principal](https://pt-br.reactjs.org/docs/conditional-rendering.html) na
> documentação oficial.

## Atributos

Assim como no HTML podemos passar atributos para os nossos elementos HTML, no
JSX podemos passar atributos para nossos elementos React.

```jsx
const link = <a href="www.djrogerinho.com.br">hackearam meu email</a>;
console.log(link);
// {
//   ...
//   type: 'a',
//   props: { href: 'www.djrogerinho.com.br', children: 'hackearam meu email' },
// }
```

Também é possível usar expressões do JavaScript como valor para nossos
atributos. Basta usar a sintaxe de chaves.

```jsx
const avatar = <img src={user.image} />;
```

> ⚠ Quando usamos JSX no React, os nomes de atributos devem ser
> escritos em `camelCase`.
