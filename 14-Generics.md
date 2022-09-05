# Generics

Generics allow us to define reusable functions and classes that work with multiple types rather than a single type.

The syntax is...not pretty. They are used all over the place, so it's best to get comfortable with them :)

```
function wrapInArray<T>(element: T): T[]{
  return [element];
}
```

Could use a function like this:

```
function doThing(thing: number | string): number | string {

}
```

But you don't know by looking at this function if it returns a number or a string.

With **Generics** we abstract the type even further.

- if you pass in a number will return a number
- if you pass a string it will return a string.

**Example of built in Generics**

```
const nums: Array<number> = []
const colors: Array<string> = []
```

---

## Another Example Of A Built-in Generic

`querySelector` is a generic function that accepts some type inside:

**HTML**

```
<input
  id="username"
  type="text"
  placeholder="username"
  value="bluesteele345"
/>
<button class="btn">Click Me</button>
```

**TS**

```
const inputEl = document.querySelector<HTMLInputElement>("#username")!;
console.dir(inputEl);
inputEl.value = "Hacked!";

const btn = document.querySelector<HTMLButtonElement>(".btn")!;;
```

---

## Writing the first Generic

We have established a relationship that says, whatever the input type is, that will be the return type

I can customize the `identity` function to work with different types. It's a generic version that says some type, and we use that within the function parameter list and the return type annotation of the function.

```
interface Cat {
  name: string;
  breed: string;
}

function identity<Type>(item: Type): Type {
  return item;
}

identity<number>(7)
identity<string>("hello")
identity<Cat>({})

```

If you provide a `string` this is what identity looks like:

```
function identity<string>(item: string): string {
  return item;
}
```

If you provide a `boolean` this is what identity looks like:

```
function identity<boolean>(item: boolean): boolean {
  return item;
}
```

If we provide `Cat`

```
function identity<Cat>(item: Cat): Cat {
  return item;
}
```

but we don't write those functions, just provide a generic type

and most of the type you actually see an uppercase T:

```
function identity<T>(item: T): T {
  return item;
}
```

---

## Writing Another Generic function

```
function getRandomElement<T>(list: T[]): T {
  const randIdx = Math.floor(Math.random() * list.length);
  return list[randIdx];
}

console.log(getRandomElement<string>(["a", "b", "c"]));
getRandomElement<number>([5, 6, 21, 354, 567, 234, 654]);

```

---

## Inferred Generic Type Parameters

The angle brackets don't actually needed. TS can infer the type of that argument.

```
getRandomElement(["a", "v", "asd"]);
```

not the case with any generic e.g. :

```
const btn = document.querySelector(".btn")!;
```

---

## Generics, Arrow Functions, & TSX Files

In a `.tsx` file when you need to write an arrow function,need to add the trailing comma after that type parameter

```
const getRandomElement = <T,>(list: T[]): T => {
  const randIdx = Math.floor(Math.random() * list.length);
  return list[randIdx];
};
```

---

## Generics With Multiple Types

The return type is the intersection between `T` and `U`

```
function merge<T, U>(object1: T, object2: U) {
  return {
    ...object1,
    ...object2,
  };
}

const comboObj = merge({ name: "colt" }, { pets: ["blue", "elton"] });

```

---

## Adding Type Constraints

`extends` keyword is used when function parameters should be an of a certain type e.g. object:

```
function merge<T extends object, U extends object>(object1: T, object2: U) {
  return {
    ...object1,
    ...object2,
  };
}
```

**Extending interfaces**

```
interface Lengthy {
  length: number;
}

function printDoubleLength<T extends Lengthy>(thing: T): number {
  return thing.length * 2;
}
```

---

## Default Type Parameters

The default type value `number` comes into play if you don't specify a type

```
function makeEmptyArray<T = number>(): T[] {
  return [];
}

const numbers = makeEmptyArray();
const booleans = makeEmptyArray<boolean>();
```

---

## Writing Generic Classes

A class that can suit different needs. We generacized playlist class.

```
interface Song {
  title: string;
  artist: string;
}

interface Video {
  title: string;
  creator: string;
  resolution: string;
}

class Playlist<T> {
  public queue: T[] = [];
  add(el: T){
    this.queue.push(el)
  }
}

const songs = new Playlist<Song>()

const videos = new Playlist<Video>()
videos.add()
```

---
