# Union Types

Union types allow us to give a value a few different possible types. If the eventual value's type is included. Typescript will be happy.

We can create a union type by using the single `|` (pipe character) to separate the types we want to include. It's like saying, "This thing is allowed to be, this, this, or this". Typescript will enforce it from there.

```
// A function with a union tpe parameter
const guessAge = (age: number | string) => {
  return "Your age is: " + age
}

// CAN pass a number or a string!
guessAge(30);
guessAge("28");

// CAN'T pass something else
guessAge({ age: 32 });
```

```
let age: number | string = 21;
age = 23
age "24"
```

```
type Point = {
  x: number;
  y: number;
}

type Loc = {
  lat: number;
  long: number;
};

let coordinates: Point | Loc = {x: 1, y: 34}
coordinates = {lat: 321.213, long: 23.334}
```

## Type Narrowing w/ Union

**Narrowing the Type** is simply doing a type check before working with a value. If your value is a string you may want to use it differently than if you got a number.

Since unions allow multiple types for a value, it's good to check what came through before working with it.

```
const isTeenager = (age: number | string) => {
  if (typeof age === "string"){
    // if age is a string, do this
    console.log(age.charAt(0) === 1);
  }
  if (typeof age === "number"){
    // if age is number, do this
    console.log(age > 12 && age < 20);
  }
}

isTeenager('20'); //false
isTeenager(13); //true
```

```
function printAge(age: number | string): void {
  console.log(`You are %{age} years old`);
}

printAge(23);
printAge("87");

function calculateTax(price: number | string, tax: number){
  // return price * tax
  // error, could be a number OR a string
  // price.replace("$", "")
  // doesn't exist on type number, price could be a number

  if(typeof price === "string"){
    price = parseFloat(price.replace("$", ""))
  }
  return price*tax;
}
```

---

## Union Types and Arrays

```
// const nums: number[] = [1,2,3,4]
// const stuff: any[] = [1,2,3,4, true, "asdas", {}]
```

```
const stuff: (number | string)[]
```

```
const coords: (Point | Loc)[] = [];
coords.push({ lat: 321.213, long: 23.334 })
```

---

## Literal Types

Literal types are not just types - but the values themselves too!

On it's own, that's not super helpful. But combine it with something like unions and you can have very fine-tuned type options for Typescript to enforce.

```
//A function with a literal+union type parameter
const giveAnswer = (answer: "yes" | "no" | "maybe") => {
  return `The answer is ${answer}.`;
}

// CAN provide one of the literals in the union
giveAnswer("no") // The answer is no.

// CAN'T provide anything else
giveAnswer("oh boy I'm not sure");
```

```
let zero: 0 = 0;
let hi: "hi" = "HI"

let mood: "Happy" | "Sad" = "Happy";
mood = "Sad";
```

```
type DayOfWeek =
  | "Monday"
  | "Tuesday"
  | "Wednesday"
  | "Thursday"
  | "Friday"
  | "Saturday"
  | "Sunday";

let today: DayOfWeek = "Monday";
```
