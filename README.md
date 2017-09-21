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


### Regras para usar `let` e `const`

* Variáveis declaradas com let podem ter seu valor reatribuído, mas não podem ser redeclaradas no mesmo escopo.

* Variáveis declaradas com const devem ter um valor inicial atribuído, mas não podem ser redeclaradas no mesmo escopo e não podem ter seu valor reatribuído.


# Template Literals

Antigamente para concatenar uma variavel precisavamos utilizar o comando `+` porem acora foi introduzido o template Literals que são string que aceitão expressões embutidas delimitadas pelo backticks (`) em vez de apóstrofo ('') ou aspas duplas ("").

Template literals podem conter marcadores representados pelas sintaxe `${expressao}`. Isso torna a construção de string _muito mais facil_.


#### Antes do ES6

```javascript
const student = {
  name: 'Richard Kalehoff',
  guardian: 'Mr. Kalehoff'
};

const teacher = {
  name: 'Mrs. Wilson',
  room: 'N231'
}

let message = student.name + ' please see ' + teacher.name + ' in ' + teacher.room + ' to pick up your report card.';
```

#### Com ES6

```javascript
const student = {
  name: 'Richard Kalehoff',
  guardian: 'Mr. Kalehoff'
};

const teacher = {
  name: 'Mrs. Wilson',
  room: 'N231'
}

let message = `${student.name} please see ${teacher.name} in ${teacher.room} to pick up your report card.`; 
```

**Muito mais simples não ??? **

Alem disso podemos utilizar varias linhas ex:

```javascript
const note = ` ${teacher.name}
    Plase excuse ${student.name}
    He is recovering from the flu.

    Thank you,
    ${student.guardian}
`;
```


>DICA: expressões embutidas no interior de template literals podem fazer mais do que apenas referenciar variáveis. Você pode executar operações, chamar funções e até mesmo usar loops dentro das expressões embutidas!



# Desestruturação (Destructuring)


### Destructuring

>Destructuring pega inspiração em linguagens como Perl e Python e permite que você especifique os elementos que deseja extrair de uma array ou de um objeto no lado esquerdo de uma atribuição. Isso pode soar um pouco estranho, mas permite chegar ao mesmo resultado de antes, porém, com muito menos código

**Antes do ES6**

```javascript
const point = [10, 25, -34];

const x = point[0];
const y = point[1];
const z = point[2];

console.log(x, y, z);
```

**Utilizando destructuring**

Ex:

```javascript

const point = [10, 25, -34];

const [x, y, z] = point;

console.log(x, y, z);

```

**Antes do ES6**

```javascript
const gemstone = {
  type: 'quartz',
  color: 'rose',
  karat: 21.29
};

const type = gemstone.type;
const color = gemstone.color;
const karat = gemstone.karat;

console.log(type, color, karat);

```


**Usando Destructuring**

```javascript
const gemstone = {
  type: 'quartz',
  color: 'rose',
  karat: 21.29
};

const {type, color, karat} = gemstone;

console.log(type, color, karat);
```


# Abreviação para object literal


Abreviação é a possibilidade de remover a redundancia de nome ex: 

**Antes do es6**

```javascript
let type = 'quartz';
let color = 'rose';
let carat = 21.29;

const gemstone = {
  type: type,
  color: color,
  carat: carat
};

console.log(gemstone);
```

>`Saídas: Object {type: "quartz", color: "rose", carat: 21.29}`

**Com ES6**

```javascript
let type = 'quartz';
let color = 'rose';
let carat = 21.29;

const gemstone = { type, color, carat };

console.log(gemstone);
```

>`Saídas: Object {type: "quartz", color: "rose", carat: 21.29}`

**Abreviação no nome dos métodos**

```javascript
let type = 'quartz';
let color = 'rose';
let carat = 21.29;

const gemstone = {
  type,
  color,
  carat,
  calculateWorth: function() {
    // calculará quanto custa nossa gemstone, baseado em suas propriedades `type`, `color` e `carat`

  }
};
```

**Abreviação para nomes de métodos**

Uma vez que você só precisa referenciar a propriedade calculateWorth para chamar a função, ter a palavra function é redundante, então ela pode ser excluída.

```javascript
let gemstone = {
  type,
  color,
  carat,
  calculateWorth() { ... }
};
```

# for...in loop

Esse for intera todos as posições contaveis do array:

Ex: 

```javascript
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const index in digits) {
  console.log(digits[index]);
}
```

```
Saídas:
0
1
2
3
4
5
6
7
8
9
```

### Problema:

> O for...in loop pode te colocar em uma enrascada quando você precisar adicionar métodos extras a uma array (ou outro objeto) porque for...in loops iteram por todas as propriedades enumeráveis, o que fará com que as propriedades adicionadas ao prototype de array também aparecerão no loop.

ex:

```javascript
Array.prototype.decimalfy = function() {
  for (let i = 0; i < this.length; i++) {
    this[i] = this[i].toFixed(2);
  }
};

const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const index in digits) {
  console.log(digits[index]);
}

```

```
Saídas:
0
1
2
3
4
5
6
7
8
9
function() {
 for (let i = 0; i < this.length; i++) {
  this[i] = this[i].toFixed(2);
 }
}
```


# Loop for...of

Você escreve um loop for...of exatamente da maneira como escreveria um loop for...in, exceto pela troca do in pelo of e pelo fato de que você não precisa de um index.

```javascript
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const digit of digits) {
  console.log(digit);
}

```

```
Saídas:
0
1
2
3
4
5
6
7
8
9
```

>**DICA:** é uma boa prática utilizar nomes no plural para objetos que são coleções de valores. Dessa forma, quando você iterar pela coleção, pode usar o singular do nome da coleção para representar um item individual contido nela. Por exemplo, for (const button of buttons) {...}.


**Você pode parar ou interromper um loop for...of a qualquer momento.**

```javascript
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const digit of digits) {
  if (digit % 2 === 0) {
    continue;
  }
  console.log(digit);
}
```

>E você não precisa se procupar, caso precise adicionar novas propriedades aos objetos. O loop for...of só vai iterar sobre os valores da coleção.

```javascript
Array.prototype.decimalfy = function() {
  for (i = 0; i < this.length; i++) {
    this[i] = this[i].toFixed(2);
  }
};

const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const digit of digits) {
  console.log(digit);
}

```

```
Saídas:
0
1
2
3
4
5
6
7
8
9
```



# Operador spread

O operador spread, escrito com 3 pontos consecutivos ( ... ), é novo no ES6 e nos permite separar o spread iterable objects (objetos iteráveis) em múltiplos elementos.

Vamos dar uma olhada em alguns exempos para entender como ele funciona.

```javascript
const books = ["Don Quixote", "The Hobbit", "Alice in Wonderland", "Tale of Two Cities"];
console.log(...books);
```


`Saídas: Don Quixote The Hobbit Alice in Wonderland Tale of Two Cities`

### Juntando 2 arrays em um: 


```javascript
/*
 * Instructions: Use the spread operator to combine the `fruits` and `vegetables` arrays into the `produce` array.
 */

const fruits = ["apples", "bananas", "pears"];
const vegetables = ["corn", "potatoes", "carrots"];

const produce = [...fruits, ...vegetables];

console.log(produce);
```


# Parâmetro rest

O parâmetro rest, também escrito com três pontos consecutivos ( ... ), permite que você represente um número indefinido de elementos como uma array. Isso pode ser útil em diversas situações.

Uma situação é a atribuição de valores de uma array para variáveis. Por exemplo,

```javascript
const order = [20.17, 18.67, 1.50, "cheese", "eggs", "milk", "bread"];
const [total, subtotal, tax, ...items] = order;
console.log(total, subtotal, tax, items);
```

>**Saídas:** 20.17 18.67 1.5 ["cheese", "eggs", "milk", "bread"]

Esse código recupera os valores da array order e os atribui a variáveis isoladas usando destructuring. total, subtotal e tax recebem os três primeiros valores da array, enquanto items é onde você deve prestar mais atenção.

Utilizando o parâmetro rest, items recebe o resto dos valores da array (no formato de uma array).


Usando o parâmetro rest

Felizmente, com a adição do parâmetro rest, você pode re-escrever a função sum() e torná-la mais legível.

```javascript
function sum(...nums) {
  let total = 0;  
  for(const num of nums) {
    total += num;
  }
  return total;
}
```


### Quiz: 

Utilize o parâmetro rest para criar uma função average() que calcula a média de uma quantidade ilimitada de números.

> DICA: teste seu código com diferentes combinações de valores. Por exemplo,

```
average(2, 6) deveria retornar 4

average(2, 3, 3, 5, 7, 10) deveria retornar 5

average(7, 1432, 12, 13, 100) deveria retornar 312.8

average() deveria retornar 0
```

```javascript
/*
 * Programming Quiz: Using the Rest Parameter (1-5)
 */

// your code goes here

function average(...values) {
    let total = 0;
    for(const value of values) {
        total += value;
    }
    
    return (total > 0 ? total / values.length : 0)
}

console.log(average(2, 6));
console.log(average(2, 3, 3, 5, 7, 10));
console.log(average(7, 1432, 12, 13, 100));
console.log(average());
```


# Funções arrow

O ES6 introduz um novo tipo de função chamada arrow. As funções arrow são muito similares a funções regulares em termos de comportamento, mas são muito diferentes em termos de sintaxe. O código a seguir manipula uma lista de nomes, convertendo cada um deles para letra maiúscula, usando uma função com a sintaxe anterior ao ES6.

**Antes do ES6:**

```javascript
const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(function(name) { 
  return name.toUpperCase();
});
```


**Depois:**

```javascript
const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(
  name => name.toUpperCase()
);

```


```javascript
const upperizedNames = ['farrin', 'fagure', 'asser'].map(
  name => name.charAt(0).toUpperCase() + name.slice(1);
);
```

```javascript
const greet = name => `Hello ${name}!`;

```

No código acima, a função arrow é armazenada na variável greet e você pode chamá-la da seguinte maneira:

```javascript
greet('Asser');

```

> Retorno: Hello Asser!


```javascript
// lista de parâmetros vazia exige parênteses
const sayHi = () => console.log('Hello Udacity Student!');
sayHi();

```
>Saídas: Hello Udacity Student!

```javascript
// múltiplos parâmetros na lista, parênteses obrigatórios!
const orderIceCream = (flavor, cone) => console.log(`Here's your ${flavor} ice cream in a ${cone} cone.`);
orderIceCream('chocolate', 'waffle');
```


>AVISO: nem tudo são flores, e existem momentos onde as funções arrow não devem ser utilizadas. Então, antes de 
apagar da sua mente a maneira tradicional de se escrever uma função, fique atento aos seguintes detalhes:

>Há um ponto de atenção com a palavra chave this nas funções arrow

>veja mais detalhes na próxima aula!

> funções arrow são apenas expressões

> não existe declaração de função arrow