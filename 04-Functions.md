# Functions

## Function Parameter types

In TypeScript, we can specify the type of function parameters in a function definition.

This allows Typescript to enforce the types for the values being passed into your function.

Typing parameters is just like typing variables!

```
function greet(person: string){
  return `Hi, ${person}`!
}
```

**Multiple variables**

```
const doSomething = (person: string, age: number, isFunny: boolean) => {};
```

**Default parameters**

```
function greet(person: string = "stranger"){
  return `Hi, ${person}`!
}
```

---

## Function Return Types

We can specify the type returned by a function. Even though TypeScript can ofter infer this, I prefer the explicit annotations.

Add the type annotation after the function parameter list.

//Creating a function with a return type

```
const addNums = (x: number, y: number): number => {
  return x + y;
}

addNums(5, 5);
// --> 10

function square(num: number):number {
  return num*num;
}
```

**Multiple types (Union)**

```
function rando(num: number){
  if(Math.random() < 0.5){
    return num.toString();
  }
  return num;
}
```

---

## Anonymous Functions

When Typescript can infer how an unnamed function is going to be called, it can automatically infer its parameters' types.

```
const numbers = [1,2,3];

// Contextual typing on an arrow function
numbers.forEach(num => {
  return num.toUppercase(); // Error!
  // .toUpperCase() doesn't work for nums
})
```

**TS can infer the type of color parameter**

```
const colors = ["red", "orange", "yellow"];
// color won't default to any because of the context
colors.map(color => {
  return color.toUpperCase()
  //color.toFixed() // Error!
})
```

---

## Void

Void is a return type for functions that don't return anything. It means just that - this function is void of any data.

Typescript can infer this type fairly well, but sometimes it may want you to annotate a function with a void return explicitly.

**A function that doesn't return anything**

```
const annoyUser = (num: number): void => {
  for(let i = 0; i < num; i++){
    alert('HIIIII!!');
  }
}
```

```
function printTwice(msg: string): void {
  console.log(msg);
  console.log(msg);
}
```

---

## Never

The never type represents values that **NEVER** occur. We might use it to annotate a function that always throws an exception, or a function that never finishes executing.

Don't confuse with void - void returns undefined or null, which is technically still a type of value. With never, a function **doesn't even finish executing**.

**A function that doesn't finish running**

```
const neverStop = (): never => {
  while(true){
    console.log("I'm still going!");
  }
}
```

**A function that throws an exception**

```
const makeError = (msg: string): never => {
  throw new Error(msg);
}
```

---
