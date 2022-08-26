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
