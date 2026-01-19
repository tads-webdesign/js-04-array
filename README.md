# js-04-array
Tutorial sobre Arrays e seus Métodos em JavaScript

## Índice
1. [Acessando Dados (A Regra do Zero)](#1-acessando-dados-a-regra-do-zero)
2. [Métodos de Modificação como uma Pilha e uma Fila](#2-métodos-de-modificação-como-uma-pilha-e-uma-fila)
3. [Métodos de Busca e Corte (Manipulação)](#3-métodos-de-busca-e-corte-manipulação)
4. [Loops, Percorrendo a Lista](#4-loops-percorrendo-a-lista)
5. [A "Tríade de Ouro": map, filter e find](#5-a-tríade-de-ouro-map-filter-e-find)
6. [Ordenação](#6-ordenação)

---

## 1. Acessando Dados (A Regra do Zero)

Em JavaScript, os arrays são indexados começando do **zero**. Isso significa que o primeiro elemento está na posição 0, o segundo na posição 1, e assim por diante.

### Exemplos:

```javascript
// Criando um array
const frutas = ['maçã', 'banana', 'laranja', 'uva', 'manga'];

// Acessando elementos (A Regra do Zero!)
console.log(frutas[0]);  // 'maçã' - primeiro elemento
console.log(frutas[1]);  // 'banana' - segundo elemento
console.log(frutas[4]);  // 'manga' - quinto elemento

// Tamanho do array
console.log(frutas.length);  // 5

// Acessando o último elemento
console.log(frutas[frutas.length - 1]);  // 'manga'

// Modificando um elemento
frutas[1] = 'morango';
console.log(frutas);  // ['maçã', 'morango', 'laranja', 'uva', 'manga']
```

**Dica:** Lembre-se sempre: o primeiro elemento está no índice 0!

---

## 2. Métodos de Modificação como uma Pilha e uma Fila

Arrays em JavaScript podem funcionar como **pilhas** (LIFO - Last In, First Out) ou **filas** (FIFO - First In, First Out).

### Métodos de Pilha (Stack):

```javascript
const numeros = [1, 2, 3];

// push() - adiciona no final
numeros.push(4);
console.log(numeros);  // [1, 2, 3, 4]

numeros.push(5, 6);  // pode adicionar múltiplos elementos
console.log(numeros);  // [1, 2, 3, 4, 5, 6]

// pop() - remove do final
const removido = numeros.pop();
console.log(removido);  // 6
console.log(numeros);   // [1, 2, 3, 4, 5]
```

### Métodos de Fila (Queue):

```javascript
const fila = ['primeiro', 'segundo', 'terceiro'];

// unshift() - adiciona no início
fila.unshift('novo primeiro');
console.log(fila);  // ['novo primeiro', 'primeiro', 'segundo', 'terceiro']

// shift() - remove do início
const atendido = fila.shift();
console.log(atendido);  // 'novo primeiro'
console.log(fila);      // ['primeiro', 'segundo', 'terceiro']

// Simulando uma fila: adiciona no final, remove do início
fila.push('quarto');    // adiciona no final
console.log(fila);      // ['primeiro', 'segundo', 'terceiro', 'quarto']
const proximo = fila.shift();  // remove do início
console.log(proximo);   // 'primeiro'
```

**Resumo:**
- `push()` - adiciona no final
- `pop()` - remove do final
- `unshift()` - adiciona no início
- `shift()` - remove do início

---

## 3. Métodos de Busca e Corte (Manipulação)

### Métodos de Busca:

```javascript
const animais = ['gato', 'cachorro', 'pássaro', 'peixe', 'cachorro'];

// indexOf() - retorna o índice da primeira ocorrência
console.log(animais.indexOf('cachorro'));  // 1
console.log(animais.indexOf('cobra'));     // -1 (não encontrado)

// lastIndexOf() - retorna o índice da última ocorrência
console.log(animais.lastIndexOf('cachorro'));  // 4

// includes() - verifica se existe (retorna true/false)
console.log(animais.includes('gato'));    // true
console.log(animais.includes('cobra'));   // false
```

### Métodos de Corte:

```javascript
const letras = ['a', 'b', 'c', 'd', 'e', 'f'];

// slice() - copia uma parte do array (NÃO modifica o original)
const parte1 = letras.slice(1, 4);  // do índice 1 até 4 (não inclui 4)
console.log(parte1);   // ['b', 'c', 'd']
console.log(letras);   // ['a', 'b', 'c', 'd', 'e', 'f'] - original intacto

const parte2 = letras.slice(2);  // do índice 2 até o final
console.log(parte2);   // ['c', 'd', 'e', 'f']

// splice() - adiciona/remove elementos (MODIFICA o original)
const cores = ['vermelho', 'verde', 'azul', 'amarelo'];

// Remove 2 elementos a partir do índice 1
const removidas = cores.splice(1, 2);
console.log(removidas);  // ['verde', 'azul']
console.log(cores);      // ['vermelho', 'amarelo']

// Adiciona elementos no índice 1
cores.splice(1, 0, 'roxo', 'laranja');
console.log(cores);  // ['vermelho', 'roxo', 'laranja', 'amarelo']

// Remove 1 elemento e adiciona outros
cores.splice(2, 1, 'rosa', 'marrom');
console.log(cores);  // ['vermelho', 'roxo', 'rosa', 'marrom', 'amarelo']
```

**Diferença importante:**
- `slice()` - **não modifica** o array original (retorna uma cópia)
- `splice()` - **modifica** o array original

---

## 4. Loops, Percorrendo a Lista

Existem várias formas de percorrer um array em JavaScript.

### Loop For Tradicional:

```javascript
const numeros = [10, 20, 30, 40, 50];

// Loop for tradicional
for (let i = 0; i < numeros.length; i++) {
    console.log(`Índice ${i}: ${numeros[i]}`);
}
// Saída:
// Índice 0: 10
// Índice 1: 20
// Índice 2: 30
// Índice 3: 40
// Índice 4: 50
```

### For...of (moderno e simples):

```javascript
const frutas = ['maçã', 'banana', 'laranja'];

// For...of - itera sobre os valores
for (const fruta of frutas) {
    console.log(fruta);
}
// Saída:
// maçã
// banana
// laranja
```

### forEach (método de array):

```javascript
const nomes = ['Ana', 'Bruno', 'Carlos'];

// forEach - executa uma função para cada elemento
nomes.forEach(function(nome, indice) {
    console.log(`${indice + 1}. ${nome}`);
});
// Saída:
// 1. Ana
// 2. Bruno
// 3. Carlos

// forEach com arrow function (mais moderno)
nomes.forEach((nome, indice) => {
    console.log(`${indice}: ${nome}`);
});
```

### While:

```javascript
const valores = [5, 10, 15, 20];
let i = 0;

while (i < valores.length) {
    console.log(valores[i]);
    i++;
}
```

---

## 5. A "Tríade de Ouro": map, filter e find

Estes três métodos são extremamente poderosos e muito usados na programação moderna.

### map() - Transforma cada elemento

O `map()` cria um **novo array** transformando cada elemento.

```javascript
const numeros = [1, 2, 3, 4, 5];

// Duplicar cada número
const duplicados = numeros.map(num => num * 2);
console.log(duplicados);  // [2, 4, 6, 8, 10]

// Criar objetos a partir de um array
const nomes = ['Ana', 'Bruno', 'Carlos'];
const usuarios = nomes.map((nome, indice) => {
    return {
        id: indice + 1,
        nome: nome
    };
});
console.log(usuarios);
// [
//   { id: 1, nome: 'Ana' },
//   { id: 2, nome: 'Bruno' },
//   { id: 3, nome: 'Carlos' }
// ]

// Extrair uma propriedade de objetos
const produtos = [
    { nome: 'Notebook', preco: 3000 },
    { nome: 'Mouse', preco: 50 },
    { nome: 'Teclado', preco: 150 }
];
const precos = produtos.map(produto => produto.preco);
console.log(precos);  // [3000, 50, 150]
```

### filter() - Filtra elementos que atendem uma condição

O `filter()` cria um **novo array** apenas com os elementos que passam no teste.

```javascript
const numeros = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Filtrar apenas números pares
const pares = numeros.filter(num => num % 2 === 0);
console.log(pares);  // [2, 4, 6, 8, 10]

// Filtrar apenas números maiores que 5
const maioresQue5 = numeros.filter(num => num > 5);
console.log(maioresQue5);  // [6, 7, 8, 9, 10]

// Filtrar produtos por preço
const produtos = [
    { nome: 'Notebook', preco: 3000 },
    { nome: 'Mouse', preco: 50 },
    { nome: 'Teclado', preco: 150 },
    { nome: 'Monitor', preco: 800 }
];
const produtosBaratos = produtos.filter(produto => produto.preco < 200);
console.log(produtosBaratos);
// [
//   { nome: 'Mouse', preco: 50 },
//   { nome: 'Teclado', preco: 150 }
// ]
```

### find() - Encontra o primeiro elemento que atende a condição

O `find()` retorna o **primeiro elemento** que passa no teste (ou `undefined` se não encontrar).

```javascript
const numeros = [5, 12, 8, 130, 44];

// Encontrar o primeiro número maior que 10
const encontrado = numeros.find(num => num > 10);
console.log(encontrado);  // 12

// Encontrar um usuário pelo ID
const usuarios = [
    { id: 1, nome: 'Ana', idade: 25 },
    { id: 2, nome: 'Bruno', idade: 30 },
    { id: 3, nome: 'Carlos', idade: 28 }
];
const usuario = usuarios.find(user => user.id === 2);
console.log(usuario);  // { id: 2, nome: 'Bruno', idade: 30 }

// Quando não encontra
const naoExiste = numeros.find(num => num > 200);
console.log(naoExiste);  // undefined
```

### Combinando a Tríade:

```javascript
const pessoas = [
    { nome: 'Ana', idade: 17, cidade: 'São Paulo' },
    { nome: 'Bruno', idade: 25, cidade: 'Rio de Janeiro' },
    { nome: 'Carlos', idade: 30, cidade: 'São Paulo' },
    { nome: 'Diana', idade: 22, cidade: 'Belo Horizonte' },
    { nome: 'Eduardo', idade: 19, cidade: 'São Paulo' }
];

// Filtrar maiores de idade de São Paulo e pegar apenas os nomes
const nomesMaioresSP = pessoas
    .filter(pessoa => pessoa.idade >= 18)
    .filter(pessoa => pessoa.cidade === 'São Paulo')
    .map(pessoa => pessoa.nome);

console.log(nomesMaioresSP);  // ['Carlos', 'Eduardo']
```

**Resumo da Tríade:**
- `map()` - **transforma** cada elemento
- `filter()` - **seleciona** elementos que atendem a condição
- `find()` - **encontra** o primeiro elemento que atende a condição

---

## 6. Ordenação

O método `sort()` ordena os elementos de um array **modificando o array original**.

### Ordenação Básica (strings):

```javascript
const frutas = ['banana', 'maçã', 'laranja', 'abacaxi'];

frutas.sort();
console.log(frutas);  // ['abacaxi', 'banana', 'laranja', 'maçã']
```

### Ordenação de Números:

```javascript
// CUIDADO! sort() converte para string por padrão
const numeros = [10, 5, 40, 25, 1000, 1];

numeros.sort();
console.log(numeros);  // [1, 10, 1000, 25, 40, 5] - ERRADO!

// Forma CORRETA de ordenar números
const numerosCorretos = [10, 5, 40, 25, 1000, 1];

// Ordem crescente
numerosCorretos.sort((a, b) => a - b);
console.log(numerosCorretos);  // [1, 5, 10, 25, 40, 1000]

// Ordem decrescente
numerosCorretos.sort((a, b) => b - a);
console.log(numerosCorretos);  // [1000, 40, 25, 10, 5, 1]
```

### Ordenação de Objetos:

```javascript
const alunos = [
    { nome: 'Carlos', nota: 7.5 },
    { nome: 'Ana', nota: 9.0 },
    { nome: 'Bruno', nota: 6.5 },
    { nome: 'Diana', nota: 8.5 }
];

// Ordenar por nota (crescente)
alunos.sort((a, b) => a.nota - b.nota);
console.log(alunos);
// [
//   { nome: 'Bruno', nota: 6.5 },
//   { nome: 'Carlos', nota: 7.5 },
//   { nome: 'Diana', nota: 8.5 },
//   { nome: 'Ana', nota: 9.0 }
// ]

// Ordenar por nome (alfabética)
alunos.sort((a, b) => a.nome.localeCompare(b.nome));
console.log(alunos);
// [
//   { nome: 'Ana', nota: 9.0 },
//   { nome: 'Bruno', nota: 6.5 },
//   { nome: 'Carlos', nota: 7.5 },
//   { nome: 'Diana', nota: 8.5 }
// ]
```

### reverse() - Inverte a ordem:

```javascript
const letras = ['a', 'b', 'c', 'd', 'e'];

letras.reverse();
console.log(letras);  // ['e', 'd', 'c', 'b', 'a']

// Combinando sort e reverse
const numeros = [3, 1, 4, 1, 5, 9, 2, 6];
numeros.sort((a, b) => a - b).reverse();
console.log(numeros);  // [9, 6, 5, 4, 3, 2, 1, 1]
```

**Dica importante:** `sort()` modifica o array original. Se você quiser manter o original, faça uma cópia primeiro:

```javascript
const original = [3, 1, 4, 1, 5];
const ordenado = [...original].sort((a, b) => a - b);

console.log(original);  // [3, 1, 4, 1, 5] - mantém a ordem original
console.log(ordenado);  // [1, 1, 3, 4, 5] - array ordenado
```

---

## Conclusão

Este tutorial cobriu os principais conceitos e métodos de arrays em JavaScript:

✅ **Acesso** - índices começam em 0  
✅ **Modificação** - push, pop, shift, unshift  
✅ **Busca e Corte** - indexOf, includes, slice, splice  
✅ **Loops** - for, for...of, forEach  
✅ **Tríade de Ouro** - map, filter, find  
✅ **Ordenação** - sort, reverse  

Arrays são fundamentais em JavaScript e dominar esses métodos vai tornar seu código mais limpo e eficiente!

---

## Recursos Adicionais

- [MDN - Array](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [JavaScript.info - Arrays](https://javascript.info/array)
- [W3Schools - JavaScript Arrays](https://www.w3schools.com/js/js_arrays.asp)
