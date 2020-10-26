> 🚧 Seção em construção

> Hooks são funções que dão superpoderes aos componentes.

# Hooks

Como nossos componentes são só funções JavaScript, não é possível guardar estado
nativamente.

```jsx
function Component() {
  let counter = 0;

  function handleClick() {
    counter = counter + 1; // não vai funcionar 😢
  }

  return (
    <div>
      <p>Você clicou {counter} vezes.</p>
      <button onClick={handleClick}>Me Clica!</button>
    </div>
  );
}
```

Vamos entender porque o exemplo acima não deve funcionar. Primeiro, quando
`Component` é renderizado pela primeira vez, o valor de `counter` será 0. Quando
um clique ocorrer no botão, a função `handleClick` será chamada, incrementando o
valor de counter.

O problema é que isso não renderiza o componente de novo. Ou seja, o React nunca
chama a função `Component` novamente para atualizar a interface com o novo
valor. Precisamos de uma forma de falar para o React _renderizar nosso componente
novamente_.

Além disso, se conseguirmos falar para o React renderizar novamente, ele
encontrará a atribuição `let counter = 0` novamente, fazendo o valor ser sempre
zero. Precisamos de um forma de falar para p React _não atribuir um valor
novamente_.

```jsx
function Component() {
  let counter = atribuaNaPrimeiraVez(0);

  function handleClick() {
    counter = counter + 1;
    renderizeNovamenteComONovoValor();
  }

  return (
    <div>
      <p>Você clicou {counter} vezes.</p>
      <button onClick={handleClick}>Me Clica!</button>
    </div>
  );
}
```

## Uma ajuda externa

O React nos provém um hook que faz justamente o que precisamos: `useState`. Esse
hook nos permite fazer uma atribuição inicial, e nos dá uma função para fazer o
componente atualizar.

> É necessário importar o `useState`:
> `import React, { useState } from "react"`

```jsx
function Component() {
  const [counter, setCounter] = useState(0); // Atribua na primeira vez

  function handleClick() {
    setCounter(counter + 1); // Atualize com o novo valor
  }

  return (
    <div>
      <p>Você clicou {counter} vezes.</p>
      <button onClick={handleClick}>Me Clica!</button>
    </div>
  );
}
```

A função `useState` retorna um array com dois valores. O primeiro é um estado
atômico que criamos. O segundo é uma função que nos ajuda a causar um nova
renderização com um valor atualizado. `useState` recebe um argumento, que é o
valor inicial do nosso estado atômico.

## O fluxo do estado

1. React executa `Component` pela primeira vez.

```jsx
function Component() {
  const counter = 0;

  function handleClick() {
    setCounter(0 + 1); // Isso vai causar uma nova renderização
  }

  return (
    <div>
      <p>Você clicou 0 vezes.</p>
      <button onClick={handleClick}>Me Clica!</button>
    </div>
  );
}
```

2. O usuário clica no botão, causando nosso `handleClick` falar para o React que
   o componente precisa ser atualiza com um novo valor de `counter`.

3. React executa `Component` pela segunda vez, atribuindo um valor atualizado
   para `counter`

```jsx
function Component() {
  const counter = 1;

  function handleClick() {
    setCounter(1 + 1); // Isso vai causar uma nova renderização
  }

  return (
    <div>
      <p>Você clicou 1 vezes.</p>
      <button onClick={handleClick}>Me Clica!</button>
    </div>
  );
}
```

A cada vez que atualizamos um estado, o componente é reexecutado com os valores
atualizados. Cada atualização, o React efetivamente cria um novo elemento.

## Uso avançado

Algumas vezes, não temos disponível o estado atual para atualizá-lo, como quando
passamos a função _setter_ para um outro componente. Nesses casos, o função
_setter_ aceita uma callback, que descreve como o estado deve mudar. Esse
callback recebe um único argumento, o valor atual do estado a ser atualizado.

```jsx
function Component() {
  const [counter, setCounter] = useState(0);

  function handleClick() {
    setCounter((c) => c + 1); // Isso é equivalente aos exemplos anteriores
  }

  return (
    <div>
      <p>Você clicou {counter} vezes.</p>
      <button onClick={handleClick}>Me Clica!</button>
    </div>
  );
}
```

O valor inicial passado para `useState` também pode ser uma função, que retorna
o valor inicial. Isso é útil quando o valor inicial é resultado de um cálculo
demorado, pois a função só será executada na primeira renderização.

```jsx
const [state, setState] = useState(() => {
  return calculoDemorado(props);
});
```

## Efeitos colaterais

Componentes React devem ser funções puras do ponto de vista de nós
desenvolvedores. Isso quer dizer que mutações no DOM, logs, e temporizadores não
devem ser usados no corpo de uma função.

```jsx
function Component() {
  const [counter, setCounter] = useState(0);

  function handleClick() {
    setCounter(counter + 1);
  }

  document.title = counter; // 💥 efeito colateral

  return (
    <div>
      <p>Você clicou {counter} vezes.</p>
      <button onClick={handleClick}>Me Clica!</button>
    </div>
  );
}
```

O exemplo acima faz uma mutação no object `document`. Isso é considerado um
efeito colateral, e da forma que escrevemos pode gerar inconsistências e
resultados inesperados.

Para executarmos efeitos, precisamos do hook `useEffect`. Esse hook nos permite
executar um código imperativo _após cada renderização_.

```jsx
function Component() {
  const [counter, setCounter] = useState(0);

  function handleClick() {
    setCounter(counter + 1);
  }

  useEffect(() => {
    document.title = counter; // 😎 agora sim
  });

  return (
    <div>
      <p>Você clicou {counter} vezes.</p>
      <button onClick={handleClick}>Me Clica!</button>
    </div>
  );
}
```

## O array de dependências

Muitas vezes, nosso efeito depende apenas de alguns `props` ou alguns estados.
Isso quer dizer que se algum outro valor mudar, nosso efeito não precisa ser
disparado, pois não **depende** desse outro valor.

```jsx
function Component() {
  const [counter, setCounter] = useState(0);
  const [name, setName] = useState("Trainee");

  function handleUpgrade() {
    setName("Cjotinha");
  }

  function handleClick() {
    setCounter(counter + 1);
  }

  useEffect(() => {
    document.title = counter; // Vou executar quando name mudar
  });

  return (
    <div>
      <h1>Olá {name}</h1>
      <p>Você clicou {counter} vezes.</p>
      <button onClick={handleClick}>Me Clica!</button>
      <button onClick={handleUpgrade}>Upgrade!</button>
    </div>
  );
}
```

No exemplo acima, nosso efeito não depende de name, já que name não aparece no
corpo da função registrada. Podemos falar para o React explicitamente quais são
as suas dependências usando um _array de dependências_.

```jsx
function Component() {
  const [counter, setCounter] = useState(0);
  const [name, setName] = useState("Trainee");

  function handleUpgrade() {
    setName("Cjotinha");
  }

  function handleClick() {
    setCounter(counter + 1);
  }

  useEffect(() => {
    document.title = counter; // 😎 agora sim
  }, [counter]);

  return (
    <div>
      <h1>Olá {name}</h1>
      <p>Você clicou {counter} vezes.</p>
      <button onClick={handleClick}>Me Clica!</button>
      <button onClick={handleUpgrade}>Upgrade!</button>
    </div>
  );
}
```

O _array de depêndecias_ contém os valores que aquele efeito precisa para
executar. Lembre-se que quando um valor atualiza, todo o componente é [executado
novamente](#o-fluxo-do-estado). Isso quer dizer que o seu array de dependências
deve conter todos os valores que aparecem no corpo da função. Omitir um valor
pode levar a comportamentos inesperados devido ao uso de valores desatualizados.

> ⚠ Não minta para o React. Seja honesto e conte para ele quais são os valores
> que o seu efeito necessita.
