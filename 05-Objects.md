# Objects

Objects can be typed by declaring what the object should look like in the annotation.

Accessing a property that isn't defined or performing operations without keeping types in mind will throw errors!

```
// A function with an object type parameter
const printName = (name: { first: string; last: string }): string => {
  return `Name: ${first} ${last}`;
}

printName({first: 'Will', last: 'Ferrell'});
//Name: Will Ferrell
```

**Object variable**

```
let coordinate:{x: number, y: number} = { x:34, y:2 };
```

**Denote object type that is returned**

```
function randomCoordinate(): {x:number, y:number} {
  return {
    x: Math.random(),
    y: Math.random()
  }
}
```

**Object literal may only specify known properties**

```
printName({first: "Mick", last: "Jagger", age 473}) // Error on age!
```

**but if**

```
const singer = {first: "Mick", last: "Jagger", age 473};
printName(singer) // No error!
```

A decision was made that if you pass inline the object literal, TS will throw an error.

But if you define it in a separate variable first, then it's only going to check that the properties that we outline and excess properties are ignored

---

## Type Alias

Instead of writing out object types in an annotation, we can declare them separately in a **type alias**, which is simply the desired shape of the object.

This allows us to make our code more readable and even reuse the types elsewhere in our code.

```
//A type alias!
type Person = {
  name; string;
  age: number;
}

//Use the type alias in the annotation
const sayHappyBirthday = (person: Person) => {
  return `Hey ${person.name}, congrats on turning ${age}`;
}

sayHappyBirthday({name: 'Jerry', age: 42});
```

**Instead of repeating that**

```
function doublePoint(point: {x: number; y: number}): {
  x: number;
  y: number;
} {
  return {x: point.x * 2, y: point.y*2};
}
```

**Use alias**

```
type Point = {
  x: number;
  y: number;
}

function doublePoint(point: Point): Point {
  return {
    x: point.x*2,
    y: point.y*2
  }
}
```

---

## Nested Objects

```
//A function with a nested object type parameter
const describePerson = (person: {
  name: string;
  age: number;
  parents : {
    mom: string;
    dad: string;
  }
}) => {
  return `Person: ${name},
  Age: ${age},
  parents: ${parentNames.mom}, ${parentNames.dad}.`;
}

describePerson({name: 'Jimmy', age: 10, parents: {mom: 'Kim', dad: 'Steve'}});
```

**Another example**

```
type Song = {
  title: string;
  artist: string;
  numStreams: number;
  credits: {
    producer: string;
    writer: string;
  };
}

function calculatePayout(song:Song): number{
  return song.numStreams * 00033
}

function printSong(song:Song): void {
  console.log(`${song.title} - ${song.artist}`)
}

const mySong: Song = {
  title: "Unchained Melody:,
  artist: "Righteous Brothers",
  numStreams: 12873321,
  credits: {
    producer: "Phil Spector",
    writer: "Alex North"
  }
}

const earnings = calculatePayout(mySong)
console.log(earnings);
printSong(mySong)
```

---

## Optional properties

```
type Point = {
  x: number;
  y: number;
  z?: number;
}

const myPoint: Point = {
  x: 1,
  y: 3,
  z: 9
}

const myPoint2: Point = {
  x: 1,
  y: 3
}
```

---

## Readonly

Special modifier in TypeScript, to mark some properties in an object, array or class as readonly and we can't change theses properties.

```
type User = {
  readonly id: number,
  username: string;
}

const user: User = {
  id: 12837,
  username: "catgurl"
}

console.log(user.id) //ok
user.id = 238974 //Error, cannot be modified
```

---

## Intersection

Having multiple types and combine them with ampersand

```
type Circle = {
  radius: number;
};

type Colorful = {
  color: string;
};

type ColorfulCircle = Circle & Colorful;

const happyFace = ColorfulCircle = {
  radius: 4,
  color: "yellow"
}

```

```
type Cat = {
  numLives: number
}

type Doc = {
  breed: string
}

type CatDog = Cat & Dog & {
  age: number
}

const christy: CatDog = {
  numLives: 7,
  breed: "Husky",
  age: 9
}
```
