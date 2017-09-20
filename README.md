# ES6 Curso

### **let** e **const**

Criados para resolver o problema de Hoisting pois no javascript todas as variaveis de uma function erá adicionada no topo da função e assim podendo ser acessada.

Com **let** e **const** isso foi resolvido e caso tente acessar uma variavel que não foi criada teremos o erro: 


```javascript
function getClothing(isCold) {
  if (isCold) {
    const freezing = 'Grab a jacket!';
  } else {
    const hot = 'It’s a shorts kind of day.';
    console.log(freezing);
  }
}
```

`ReferenceError: freezing is not defined`


