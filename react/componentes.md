> 🚧 Seção em construção

# Componentes

Componentes são funções que recebem um argumento, chamado de props `props` e
retornam JSX. Na próxima seção, veremos como usar `hooks` para dar superpoderes
para os nossos componentes.

```jsx
function Componente = ({ ...props }) => {
  return <h1>Olá {props.name}</h1>
}
```

Para usarmos nossos _componentes_ dentro do JSX, basta usá-los como tags. Os
atributos que passaremos para esse componente serão transformados em props.

```jsx
const App = () => {
  return <Componente name="Trainee"></Componente>;
};
```

> 💡 React diferencia entre elementos nativos do DOM, como `h1` ou `div`, e
> componentes React baseado no capitalização do nome. Isso quer dizer que
> `<componente />` será interpretado como uma tag HTML, mesmo que exista uma
> função `componente` no escopo.

## Children
