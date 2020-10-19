# Componentes

> UI = F(data) - Equação Fundamental do React

Componentes são funções que recebem entradas arbitrárias, chamadas "props", e retornam uma marcação, que representa o que deve ser mostrado na tela.

```javascript
function Example(props) {
  return <h1>Olá, {props.name}</h1>;
}
```

## Usando um componente

Usando o JSX, também é possível incluir nossos componentes no DOM
