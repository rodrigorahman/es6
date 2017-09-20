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