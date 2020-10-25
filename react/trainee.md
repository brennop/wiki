# Trainees das Galáxias

React é um framework para desenvolvimento de aplicações web e nativas. Seu foco
é em facilitar para o desenvolvedor criar interfaces interativas sem se
preocupar com o código que orquestra essas interações.

## Projeto React

É possível iniciar um projeto React usando o [Create React App](https://create-react-app.dev/) ou usando o [CodeSandbox](https://codesandbox.io).

Para iniciar um novo projeto React na pasta _projeto_, basta usar o comando

```bash
yarn create react-app projeto
```

ou

```bash
npx create-react-app projeto
```

## JSX

É uma sintaxe para o JavaScript que permite descrever a nossa interface junto da
nossa lógica. Usando o JSX, podemos escrever _Elementos_, que podem ser tags
HTML, dentro do nosso código JavaScript.

```jsx
const element = <h1>Olá Mundo</h1>;
```

Quando rodamos nossa aplicação React, um _renderer_, como o ReactDOM, trata de
avaliar nossos elementos e colocá-los na tela.

## Expressões

Podemos inserir qualquer [expressão
JavaScript](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Guide/Expressions_and_Operators)
válida dentro de chaves no JSX.

```jsx
const name = "Trainee";
const element = <h1>Olá, {name}</h1>; // <h1>Olá, Trainee</h1>
```

## Atributos

Usando JSX podemos passar argumentos para nossos elementos, usando o nome do
atributo e uma atribuição de valor.

```jsx
const link = <a href="https://pt-br.reactjs.org">Documentação do React</a>;
```

> No React, atributos de elementos do DOM devem ser escritos com `camelCase`.
> Por exemplo, escreveríamos `tabIndex` ao invés de `tabindex` e `className` ao
> invés de `class`.

## Componentes

São funções JavaScript que retornam [_elementos_](#jsx). Todo componente também
é um elemento. Por convenção, componentes são escritos capitalizados.

```jsx
function Componente() {
  return <h1>Olá Mundo</h1>;
}
```

Para usar componentes que definimos, basta colocá-lo entre bicudinhos `<>`, com
o mesmo nome da função que os define.

```jsx
function App() {
  return <Componente></Componente>;
}
```

## Renderização

Componentes também são elementos. Isso quer dizer que quando nossa aplicação
React é executada, um _renderer_ irá executar nossos componentes para colocá-los
na tela. Chamamos o processo de execução dos nossos componentes para obter o JSX
final de **renderização**.

> Não confunda renderização com mostrar na tela. Quando o React renderiza os
> componentes, apenas os transforma em objetos que serão mais tarde colocados na
> tela pelo browser, ou outro host, num processo chamdo de _pintura_.

## Props

São atributos que passamos para um componentes. Os componentes recebem _props_
como primeiro argumento da função que os define. Esse argumento contém um objeto
com todos os atributos passados ao elemento React.

```jsx
function BemVindo(props) {
  return <h1>Bem Vindo, {props.name}</h1>;
}
```

Para atribuir valor a instância de um componente, fazemos assim como passamos
[atributos](#atributos) para elementos React.

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

Por padrão, o React passa um atributo para todos os elementos chamado
`children`. Esse atributo contém os filhos daquela instância do componente
definidos na marcação JSX.

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

Para o primeiro botão, `props.children` conterá um elemento de texto com o valor
"Prosseguir", e para o segundo botão, o valor será "Cancelar".

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

O hook `useState` é uma função que recebe um estado inicial, e retorna um array
contendo o valor atual desse estado e uma função helper, que permite alterar
esse estado. Precisamos dessa função helper porque o estado no React é
_imutável_. Esse hook permite guardar de forma simples um valor dentro de um
componente React.

```jsx
function Counter() {
  const [counter, setCounter] = React.useState(0);

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

### useEffect

Funções também não tem ciclo de vida, ou seja, não sabemos se um componente está
sendo renderizado pela primeira vez ou pela décima. O hook `useEffect` nos
possibilita registrar uma função para rodar a cada update do componente. Um
update ocorre toda vez que uma de suas dependências, uma prop ou um estado por
exemplo, é alterado.

```jsx
function Counter() {
  const [name, setName] = React.useState("");

  useEffect(() => {
    console.log(name); // executa toda vez que name mudar
  });

  const handleChange = (event) => {
    setName(event.target.value);
  };

  return (
    <div>
      <input name="name" onChange={handleChange} />
    </div>
  );
}
```

O hook `useEffect` espera dois argumentos, uma função para ser registrada, e um
array de dependências opcional. A cada update o `useEffect` checa o valor de
suas dependências, e execute a função registrada caso algum tenha mudado. Por
via de regra, é importante incluir todos os valores do qual seu efeito depende
no array de dependências.

```jsx
  const [name, setName] = useState("");
  const [firstName, setFirstName] = useState("");

  useEffect(() => {
    setFirstName(name.split(" ")[0]);
  }, [name]);
}
```

No exemplo acima, o efeito só irá executar quando name tiver seu valor alterado.
Isso é útil para evitar loops infinitos, já que a chamada de `setFirstName`
causará um update no componente.

> Podemos usar um array de dependências vazio para indicar que o efeito deve ser
> executado apenas na primeira vez que o componente for montado na tela.
