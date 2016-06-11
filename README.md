# geneticalgorithm

## Introduction
This provides you heuristic algorithm depends on [genetic algoritm](https://en.wikipedia.org/wiki/Genetic_algorithm) to find one of the best solution for problem of arrangement objects.

To make this, you need to provide:

**objects array** that you want to compare, (*for genetic*: this will give chromosomes to generate genes for solutions)

**cost function** which return costs for specific arrangement of objects in array (*for genetic*: this determines the value of solution in population, *smaller mean better*).

## Getting started
To import algorithm to your projects write
```bash
git clone https://github.com/bobbylej/geneticalgorithm.git

```
or download zip.

**genetic.es6.js** is written with ECMAScript6

## Using
```js
let genetic = new GeneticAlgorithm( genes, costFunction, config );
// find result (best solution)
let result = genetic.result();

// result is also saved in variable genetic.result
result === genetic.result;
```
- **genes** - our array of objects (*chromosomes*),
- **costFunction** - function with parameter **genes** to count cost of specific arrangement of genes (*remember: smaller mean better*),
- **config** - json object for advanced options,
  - **populationSize** - (*default: 500*) amount of generated populations (various arrangement of genes),
  - **amount** - (*default: 300*) amount of iterations to find the best solution. More iterations can give better solution, but also will take longer time,
  - **mutateProb** - (*default: 0.7*) probability of making mutation on genes from

## Example
As an example I will show you solution for [TSP](https://en.wikipedia.org/wiki/Travelling_salesman_problem).
To simplify, assume that distance between the cities is equal to the difference of their ID's (**costFunction**).
```js
let cities = [];
for( let i = 1; i < 100; i++ ) {
  cities.push(i);
}

costFunction = ( genes ) => {
  let cost = 0;
  for( let i = 0; i < genes.length; i++ ) {
    if( i === 0 ) {
      cost += Math.abs(genes[genes.length-1] - genes[i]);
    }
    else {
      cost += Math.abs(genes[i] - genes[i-1]);
    }
  }
  return cost;
}

console.log( 'Start Algorithm...' );
let genetic = new GeneticAlgorithm( cities, costFunction, {
  populationSize: 500,
  amount: 300,
  mutateProb: 0.7
});

let result = genetic.result();

console.log( 'STOP' );
console.log( 'Result:', result );
```
As you can see, it is very easy!
