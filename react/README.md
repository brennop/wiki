# Trainees das Galáxias

React é um framework para desenvolvimento de aplicações web e nativas. Seu foco é em facilitar para o desenvolvedor criar interfaces interativas sem se preocupar com o código que orquestra essas interações.

## JSX

É uma sintaxe para o JavaScript que permite descrever a nossa interface junto da nossa lógica. Usando o JSX, podemos escrever _Elementos_, que podem ser tags HTML, dentro do nosso código JavaScript.

```jsx
const element = <h1>Olá Mundo</h1>;
```

## Expressões

## Atributos

Usando JSX podemos passar argumentos para nossos elementos, usando o nome do atributo e uma atribuição de valor.

```jsx
const link = <a href="https://pt-br.reactjs.org">Documentação do React</a>;
```

> No React, atributos de elementos do DOM devem ser escritos com `camelCase`. Por exemplo, escreveríamos `tabIndex` ao invés de `tabindex` e `className` ao invés de `class`.

## Componentes

São funções JavaScript que retornam [_elementos_](#jsx). Todo componente também é um elemento. Por convenção, componentes são escritos capitalizados.

```jsx
function Componente() {
  return <h1>Olá Mundo</h1>;
}
```

Para usar componentes que definimos, basta colocá-lo entre bicudinhos `<>`, com o mesmo nome da função que o define.

```jsx
function App() {
  return <Componente></Componente>;
}
```

## Props

São atributos que passamos para um componentes. Os componentes recebem _props_ como primeiro argumento da função que os define. Esse argumento contém um objeto com todos os atributos passados ao elemento React.

```jsx
function BemVindo(props) {
  return <h1>Bem Vindo, {props.name}</h1>;
}
```

Para atribuir valor a instância de um componente, fazemos assim como passamos [atributos](#atributos) para elementos React.

```jsx
function App() {
  return <BemVindo name="Trainee" />;
}
```

O código acima deve rederizar a seguinte marcação em HTML.

```jsx
<h1>Bem Vindo, Trainee</h1>
```

## Children

Por padrão, o React passa um atributo para todos os elementos chamado `children`. Esse atributo contém os filhos daquela instância do componente definidos na marcação JSX.

```jsx
function Button(props) {
  return <button className="btn">{props.children}</button>;
}

function App() {
  return (
    <div>
      <Button>Prosseguir</Button>
      <Button>Cancelar</Button>
    </div>
  );
}
```

Para o primeiro botão, `props.children` conterá um elemento de texto com o valor "Prosseguir", e para o segundo botão, o valor será "Cancelar".

## Eventos

Podemos atribuir listeners de eventos à um elemento do DOM de forma simples no
React. Para fazer isso, basta definir uma função, o handler do evento, e
passá-la como valor para o atributo que representa o evento. Uma lista de
atributos de eventos do React pode ser encontrada
[aqui](https://pt-br.reactjs.org/docs/events.html#supported-events).

```jsx
function Component() {
  function handleClick(event) {
    alert("Me Clicou!");
  }

  return <button onClick={handleClick}>Me Clica!</button>;
}
```

A função handler recebe um objeto event, que representa um
[SyntheticEvent](https://pt-br.reactjs.org/docs/events.html) do React. Esse
objeto contém informações relevantes sobre o evento, como o elemento do DOM que
o chamou e funções para manipular o evento.

## Hooks

Por si só, funções não são capazes de guardar um estado no JavaScript. Isso quer
dizer que o seguinte código não irá funcionar.

```jsx
function Component() {
  let counter = 0;

  function handleClick() {
    counter = counter + 1; // não vai funcionar 😢
  }

  return (
    <div>
      <span> Esse botão foi clicado {counter} vezes.</span>
      <button onClick={handleClick}>Me Clica!</button>
    </div>
  );
}
```

Sempre que `handleClick` for chamado, o valor de `counter` deverá aumentar, mas
não veremos esse resultado na tela. Isso acontece porque se o componente for
chamado novamente para atualizar o resultado na tela, estaremos atribuindo
novamente o valor 0 ao contador.

Por causa dessa limitação, precisamos de uma ajuda do React para conseguir
guardar estado dentro de um componente. Essa ajuda são os Hooks, uma API do
React para lidar com estado, ciclo de vida e outras coisa dentro de funções.

### useState

`useState` é uma função que recebe um estado inicial, e retorna um array
contendo o valor atual desse estado e uma função helper, que permite alterar
esse estado. Precisamos dessa função porque o estado no React é _imutável_. Esse
hook permite guardar de forma simples um valor dentro de um componente React.

```jsx
function Counter() {
  const [counter, setCounter] = useState(0);

  function handleClick() {
    setCounter(counter + 1); // agora vai 😄
  }

  return (
    <div>
      <span> Esse botão foi clicado {counter} vezes.</span>
      <button onClick={handleClick}>Me Clica!</button>
    </div>
  );
}
```
