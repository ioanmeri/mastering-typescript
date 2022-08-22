# Array Types

Arrays can by typed using a type annotation followed by empty array brackets, like `number[]` for an array of numbers.

Note: these arrays only allow data of that one type inside them. More on that later.

```
//Using Brackets:
//string array
let names: string[] = ["hello", "world"];
//number array
let ages: number[] = [24, 32, 19, 29];

//An alternate syntax:
//string array
let names: Array<string> = ["hello", "world"];
//number array
let ages: Array<number> = [24, 32, 19, 29]
```

More

```
const activeUsers: [] = []; // this is of type empty array
activeUsers.push("username") // error
```

**TS will annotate empty array to any type**

```
const activeUsers = []
```

---

## More Array Syntax

```
type Point = {
  x: number,
  y: number
}
```

**Array of Point objects**

```
const coords: Point[] = []
coords.push({x: 23, y:8});
```

## Multi dimensional array

```
const board: string[][] = [
  ["X", "0", "X"],
  ["X", "0", "X"],
  ["X", "0", "X"]
]
```

## Exercise

```
// **********************************************
// ******************* PART 1 *******************
// **********************************************
// Create an empty array of numbers called "ages":

const ages: number[] = [];

// **********************************************
// ******************* PART 2 *******************
// **********************************************
// Create an array variable called gameBoard that starts as an empty array.
// It should be typed to hold a 2 dimensional array of strings

const gameBoard: string[][] = []

// **********************************************
// ******************* PART 3 *******************
// **********************************************
// Create a Product type that contains a name and a price.
// An example product could be:
// {name: "coffee mug", price: 11.50}

type Product = {
  name: string;
  price: number;
}


// **********************************************
// ******************* PART 4 *******************
// **********************************************
// Write a function called getTotal that accepts an array of Product types
// It should return the sum of all the products' prices

const getTotal = (products: Product[]): number => {
  let total = 0;
  products.forEach(product => total += product.price);
  return total;
}


```
