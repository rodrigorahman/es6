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


## Contexto This in Arrow Functions

```javascript
// constructor
function IceCream() {
  this.scoops = 0;
}

// adds scoop to ice cream
IceCream.prototype.addScoop = function() {
  setTimeout(() => { // an arrow function is passed to setTimeout
    this.scoops++;
    console.log('scoop added!');
  }, 0.5);
};

const dessert = new IceCream();
dessert.addScoop();
``` 

Como as funções arrow herdam this do escopo onde estão contidas, esse código funciona!

```javascript
console.log(dessert.scoops);
```

```javascript
Imprime:
1

```

Sim, isso não funciona pelo mesmo motivo - as funções arrow herdam o valor de this do contexto onde estão inseridas. Fora do escopo do método addScoop(), o valor de this é o objeto global; portanto, se addScoop() é uma função arrow, o valor de this em seu contexto interno é o objeto global.


# Parâmetros de função default

Parâmetros de função default são muito fáceis de ler, já que ficam na lista de parâmetros da função:

```javascript
function greet(name = 'Student', greeting = 'Welcome') {
  return `${greeting} ${name}!`;
}

greet(); // Welcome Student!
greet('James'); // Welcome James!
greet('Richard', 'Howdy'); // Howdy Richard!

```


>Saídas:  
>Welcome Student!  
>Welcome James!  
>Howdy Richard!  


# Default Array destructuring

É possível combinar de parâmetros default a destructuring para criar funções muito poderosas!

```javascript
function createGrid([width = 5, height = 5]) {
  return `Generates a ${width} x ${height} grid`;
}

createGrid([]); // Generates a 5 x 5 grid
createGrid([2]); // Generates a 2 x 5 grid
createGrid([2, 3]); // Generates a 2 x 3 grid
createGrid([undefined, 3]); // Generates a 5 x 3 grid
```

>**Retornos:**  
>Generates a 5 x 5 grid   
>Generates a 2 x 5 grid   
>Generates a 2 x 3 grid  
>Generates a 5 x 3 grid  


`createGrid(); // throws an error`


>**Uncaught TypeError:** Cannot read property 'Symbol(Symbol.iterator)' of undefined

Isso gera um erro porque createGrid() espera uma array como parâmetro, para que possa realizar o processo de destructuring. Uma vez que a função foi chamda sem passar uma array, ocorre um erro, mas podemos utilizar parâmetros de função default a fim de resolver o problema!

```javascript
function createGrid([width = 5, height = 5] = []) {
  return `Generating a grid of ${width} by ${height}`;
}
```

Repare no novo = [] na lista de parâmetros da função. Se createGrid() for chamada sem nenhum argumento, o valor default será utilizado, ou seja, uma array vazia será passada como parâmetro. Caso o método receba a array vazia, não há valores para fazer o destructuring e atribuir às variáveis width e height, então, seus valores padrão serão aplicados. Assim, adicionando o = [] como o default para o parâmetro inteiro, o código a seguir funcionará:

`createGrid(); // Generates a 5 x 5 grid`

>**Retorno:** Generates a 5 x 5 grid

```javascript
/*
 * Programming Quiz: Using Default Function Parameters (2-2)
 */
function buildHouse({floors = 1, color = 'red', walls = 'brick'} = {}) {
    
    return `Your house has ${floors} floor(s) with ${color} ${walls} walls.`;
}

/* tests*/
console.log(buildHouse()); // Your house has 1 floor(s) with red brick walls.
console.log(buildHouse({})); // Your house has 1 floor(s) with red brick walls.
console.log(buildHouse({floors: 3, color: 'yellow'})); // Your house has 3 floor(s) with yellow brick walls.
```

# Classes no ES6

Este é um exemplo de como a mesma classe Plane seria escrita com a nova sintaxe de class:

```javascript
class Plane {
  constructor(numEngines) {
    this.numEngines = numEngines;
    this.enginesActive = false;
  }

  startEngines() {
    console.log('starting engines…');
    this.enginesActive = true;
  }
}
```


# Como criar um map

Para criar um map, basta digitar:

```javascript
const employees = new Map();
console.log(employees);

```

>Map {}

Isso cria um map employee, sem nenhum par chave-valor.

### Modificando maps

Diferentemente dos sets, você não pode criar maps a partir de uma lista de valores; em vez disso, você adiciona pares de chave-valor utilizando o método .set().

```javascript
const employees = new Map();

employees.set('james.parkes@udacity.com', { 
    firstName: 'James',
    lastName: 'Parkes',
    role: 'Content Developer' 
});
employees.set('julia@udacity.com', {
    firstName: 'Julia',
    lastName: 'Van Cleve',
    role: 'Content Developer'
});
employees.set('richard@udacity.com', {
    firstName: 'Richard',
    lastName: 'Kalehoff',
    role: 'Content Developer'
});

console.log(employees);
```


# Trabalhando com maps

Depois de construir seu map, você pode utilizar o método .has() para checar se um par chave-valor existe, passando a chave como parâmetro.

```javascript
const members = new Map();

members.set('Evelyn', 75.68);
members.set('Liam', 20.16);
members.set('Sophia', 0);
members.set('Marcus', 10.25);

console.log(members.has('Xavier'));
console.log(members.has('Marcus'));

```

>false  
>true

E você também pode recuperar valores contidos em um map, utilizando o método .get() e passando a chave como parâmetro.

`console.log(members.get('Evelyn'));`

>75.68


### Usando um loop 'forEach'

Sua última opção para percorrer um map é com o método .forEach().

`members.forEach((value, key) => console.log(value, key));`

> 'Evelyn' 75.68  
> 'Liam' 20.16  
> 'Sophia' 0  
> 'Marcus' 10.25  

# Promises


ex:

```javascript
new Promise(function (resolve, reject) {
    window.setTimeout(function createSundae(flavor = 'chocolate') {
        const sundae = {};
        // request ice cream
        // get cone
        // warm up ice cream scoop
        // scoop generous portion into cone!
        if ( /* iceCreamConeIsEmpty(flavor) */ ) {
            reject(`Sorry, we're out of that flavor :-(`);
        }
        resolve(sundae);
    }, Math.random() * 2000);
});

```


Esse objeto possui um método .then(), que pode ser utilizado para nos informar se a requisição realizada na promise foi concluída com sucesso ou falhou. O método .then() recebe duas funções:

* uma função para executar caso a requisição tenha sido concluída com sucesso
* uma função para executar caso a requisição tenha falhado

```javascript
mySundae.then(function(sundae) {
    console.log(`Time to eat my delicious ${sundae}`);
}, function(msg) {
    console.log(msg);
    self.goCry(); // not a real method
});

```


# Proxy

### Armadilha get

A armadilha get é utilizada para "interceptar" chamadas a propriedades:

```javascript
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        console.log(target); // the `richard` object, not `handler` and not `agent`
        console.log(propName); // the name of the property the proxy (`agent` in this case) is checking
    }
};
const agent = new Proxy(richard, handler);
agent.status; // logs out the richard object (not the agent object!) and the name of the property being accessed (`status`)
```

### Acessando o objeto-alvo de dentro do proxy

Se quiséssemos acessar de fato a propriedade, nós teriamos que retornar o valor dela por meio do objeto-alvo (target):

```javascript
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        console.log(target);
        console.log(propName);
        return target[propName];
    }
};
const agent = new Proxy(richard, handler);
agent.status; // (1)logs the richard object, (2)logs the property being accessed, (3)returns the text in richard.status
```

### Obtendo a informação de return do proxy diretamente

Como alternativa, podemos utilizar o proxy para fornecer feedback imediato:

```javascript
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        return `He's following many leads, so you should offer a contract as soon as possible!`;
    }
};
const agent = new Proxy(richard, handler);
agent.status; // returns the text `He's following many leads, so you should offer a contract as soon as possible!`
```


### **A armadilha set** é utilizada para interceptar o código que modificará uma propriedade. Ela recebe:

* o objeto-alvo do proxy
* a propriedade que está sendo alterada
* o novo valor para o proxy

```javascript
const richard = {status: 'looking for work'};
const handler = {
    set(target, propName, value) {
        if (propName === 'payRate') { // if the pay is being set, take 15% as commission
            value = value * 0.85;
        }
        target[propName] = value;
    }
};
const agent = new Proxy(richard, handler);
agent.payRate = 1000; // set the actor's pay to $1,000
agent.payRate; // $850 the actor's actual pay

```

No código acima, observe que a armadilha set checa se a propriedade payRate está sendo alterada. Se estiver, então o proxy (variável agent) reduz o valor em quinze por cento, caso a variável payRate tenha recebido algum valor pelo proxy. No fim do trecho de código, a propriedade payRate possui o valor 850.


### Outras armadilhas

Até aqui, nós vimos as armadilhas get e set (que provavelmente são as mais utilizadas), mas existem um total de 13 armadilhas diferentes que podem ser utilizadas no handler de um proxy!

>get - permite que o proxy controle chamadas para acesso à propriedades  
>set - permite que o proxy controle alterações de valor da propriedade  
>apply - permite que o proxy controle quando o objeto-alvo é invocado (o objeto-alvo é uma função)  
>has - permite que o proxy controle o uso do operador in  
>deleteProperty - permite que o proxy controle quando uma propriedade é deletada  
>ownKeys - permite que o proxy controle quando todas as chaves são requisitadas  
>construct - permite que o proxy controle quando o proxy é utilizado com a palavra-chave new, como um construtor  
>defineProperty - permite que o proxy controle quando defineProperty é utilizado para criar uma nova propriedade no objeto  
>getOwnPropertyDescriptor - permite que o proxy controle a recuperação da descrição da propriedade  
>preventExtenions - permite que o proxy controle chamadas ao Object.preventExtensions() no objeto proxy  
>isExtensible - permite que o proxy controle chamadas ao Object.isExtensible no objeto proxy  
>getPrototypeOf - permite que o proxy controle chamadas ao Object.getPrototypeOf no objeto proxy  
>setPrototypeOf - permite que o proxy controle chamadas ao Object.setPrototypeOf no objeto proxy  



# Generator Functions! 

Se quisermos ter a capacidade de pausar uma função no meio de sua execução, precisaremos de um novo tipo de função presente no ES6 - generator functions! Vamos ver como uma funciona:

```javascript
function* getEmployee() {
    console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        console.log( name );
    }

    console.log('the function has ended');
}
```

### Executando a função:

```javascript
const generatorIterator = getEmployee();
generatorIterator.next();
```

### A palavra-chave 'yield'

A palavra-chave yield foi introduzida ao ES6. Ela pode ser utilizada no interior de generator functions e é o que causa a pausa do generator. Vamos adicionar o yield ao nosso generator e fazer uma tentativa:

```javascript
function* getEmployee() {
    console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        console.log(name);
        yield;
    }

    console.log('the function has ended');
}

```

Observe que, agora, há uma palavra yield no interior do loop for...of. Se nós executarmos o generator (o que produz um iterator) e chamarmos a função **.next()**, receberemos o seguinte output:

```javascript
const generatorIterator = getEmployee();
generatorIterator.next();
```


>Logará no console:  
>the function has started  
>Amanda  
>A execução da função pausou! Mas, para ter certeza, vamos checar a próxima iteração:  

```javascript
generatorIterator.next();
```

>Logorá no console:  
>Diego

Então, a função é retomada exatamente de onde parou, recuperando o próximo item da array (Diego) na segunda chamada do método .next() e pausando a função novamente.

Agora que a funcionalidade de pausa está funcionando, o que aconteceria se pudéssemos mandar informações para o mundo "externo" de dentro da função generator? Isso é possível com yield.

Usando o yield para enviar dados ao mundo externo 

Em vez de logar no console os nomes e pausar a função, vamos utilizar o "return" para devolver o nome na array e pausar.


```javascript
function* getEmployee() {
    console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        yield name;
    }

    console.log('the function has ended');
}
```

Observe que, agora, em vez de executar console.log(name);, fazemos yield name;. Com essa mudança, ao executar o generator, o nome será devolvido para a função e a execução pausará. Vejamos esse comportamento em ação:


```javascript
const generatorIterator = getEmployee();
let result = generatorIterator.next();
result.value // is "Amanda"

generatorIterator.next().value // is "Diego"
generatorIterator.next().value // is "Farrin"
```



# Navegadores 

Como saber quais são as funcionalidades suportadas pelos navegadores?
Com novas especificações na linguagem saindo todos os anos e navegadores sendo atualizados logo em seguida, é um desafio saber qual navegador tem suporte para qual funcionalidade da linguagem. Cada fabricante de navegadores (exceto o Safari) possui um site onde é possível acompanhar seu estágio de desenvolvimento. Acompanhe as atualizações de cada navegador:  

Google Chrome - https://www.chromestatus.com/features#ES6  
Microsoft Edge - https://developer.microsoft.com/en-us/microsoft-edge/platform/status/?q=ES6  
Mozilla Firefox - https://platform-status.mozilla.org/  
OBSERVAÇÃO: o Safari não possui uma página de status, porém, por debaixo dos panos, ele utiliza um mecanismo open source de navegação, o Webkit. O status de desenvolvimento do Webkit e suas funcionalidade podem ser encontrados aqui.  
Isso pode ser muita informação para acompanhar. Se você preferir checar uma análise mais completa de todas as funcionalidades e compatibilidades de navegadores com as features do JavaScript, dê uma olhada na Tabela de compatibilidade ECMAScript, contruída por @kangax:  

http://kangax.github.io/compat-table/es6/


# Polyfills

Lista Completa: 

https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills



# Babel

O transpiler JavaScript mais popular é chamado Babel.

O nome original do Babel era um pouco mais descritivo - 6to5. Ele tinha esse nome porque sua proposta original era converter código ES6 para ES5, mas, agora, o Babel faz muito mais. Ele converterá ES6 para ES5, JSX para JavaScript e Flow para JavaScript.

Antes de olharmos o transpiling de código em nosso computador, vamos testar rapidamente o transpiling de código ES6 para ES5 diretamente no site do Babel. Vá até o Babel's REPL e cole o código a seguir no seção da esquerda




