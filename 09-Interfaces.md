# Interfaces

Interfaces serve almost the exact same purpose as type aliases (with a slightly different syntax).

We can use them to create reusable, modular types that describe the **shapes of objects**

```
//An interface!
interface Person {
  name: string;
  age: number;
}

//Use the type alias in the annotation
const sayHappyBirthday = (person: Person) => {
  return `Hey ${person.name}, congrats on turning ${age}`;
}

sayHappyBirthday({name: 'Jerry', age: 42})
```

```
interface Point {
  x: number;
  y: number;
}

const pt: Point = {x: 123, y: 1234}
```

## Optional Properties

Using question mark before the type

```
interface Person {
  first: string;
  last: string;
  nickname?: string;
}

const thomas: Person = {first: "Thomas", last: "Hardy", nickname: "Tom"}
```

## Read only properties

```
interface Person {
  readonly id: number;
  first: string;
  last: string;
  nickname?: string;
}

const thomas: Person = {first: "Thomas", last: "Hardy", nickname: "Tom", id: 21837}

**cannot assign to id because it's a readonly property**

```

## Interface methods

```
interface Person {
  readonly id: number;
  first: string;
  last: string;
  nickname?: string;
  sayHi: () => string;
  // sayHi(): string;// the same
}

const thomas: Person = {
  first: "Thomas",
  last: "Hardy",
  nickname: "Tom",
  id: 21837,
  sayHi: () => {
    return "Hello!"
  }
}
```

## Interface method parameters

discount variable name doesn't matter

```
interface Product {
  name: string;
  price: number;
  applyDiscount(discount: number): number;
}

const shoes: Product = {
  name: "Blue Suede Shoes",
  price: 100,
  applyDiscount(amount: number){
    const newPrice = this.price * (1 - amount)
    this.price = newPrice;
    return this.price
  }
}

shoes.applyDiscount(.4);
```

## Reopening interface

add new properties after already describe an interface

```
interface Person {
  name: string;
}

interface Person {
  age: number;
}

const person: Person {
  name: "Jerry",
  age: 42
}
```

**another example**

```
interface Dog {
  name: string;
  age: number;
}

interface Dog {
  breed: string;
  bark(): string;
}

const elton: Dog = {
  name: "Elton",
  age: 0.5,
  breed: "Australian Shepherd",
  bark(){
    return "WOOF WOOF!";
  }
}
```

## Extending interfaces

inhering functionality from another interface

```
interface ServiceDog extends Dog {
  job: "drug sniffer" | "bomb" | "guide dog"
}

const chewy: ServiceDog = {
  name: "Chewy"
  age: 4.5,
  breed: "Lab",
  bark(){
    return "Bark!"
  },
  job: "guide dog"
}
```

## Interface multiple inheritance

```
interface Human {
  name: string
}

interface Employee {
  readonly id: number;
  email: string
}

interface Engineer extends Human, Employee {
  level: string,
  languages: string[]
}

const pierre: Engineer = {
  name: "Pierre",
  id: 12397,
  email: "pierre@gmain.com",
  level: "senior",
  languages: ["JS", "Python"]
}
```

## Interfaces Vs. Type Aliases

- Interfaces can only describe the shape of an object

```
type Color = "red" | "blue" // cannot do union literal with interface
```

- Can reopen interfaces, cannot do that with types

```
interface Chicken = {
  breed: string
}

//cannot do same with type
interface Chicken = {
  numEggs: number
}
```

- cannot extend with types (but can use intersection types with `&`)

**Types**

```
type Name = {
  name: string;
}

type Person = Name & {
  age: number;
}

//Person took Name and added an age property!
const person: Person = {
  name: 'Jerry',
  age: 42
}
```

**Interfaces**

```
interface Name {
  name: string;
}

interface Person extends Name {
  age: number;
}

//Person took Name and added on age property!
const person: Person = {
  name: 'Jerry',
  age: 42
}
```
