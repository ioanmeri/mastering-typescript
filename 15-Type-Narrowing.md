# Type Narrowing

## Typeof Guards

**typeof Type Guards** involve simply doing a type check before working with a value.

Since unions allow multiple types for a value, we can first check what came through before working with it.

```
const isTeenager = (age: number | string) => {
    if (typeof age === 'string'){
        //if age is a string, do this
        console.log(age.charAt(0) === 1);
    }
    if (typeof age === 'number'){
        // if age is a number do this
        console.log(age > 12 && age < 20);
    }
}

isTeenager('20'); // false
isTeenager(13); //true
```

**Different types**

```
typeof "asd" // 'string'
typeof 234 // 'number'
typeof [2,3,4] // 'object'
```

**Type narrowing example**

It's not only analyzing the conditionals, it's also analyzing the `return` statements

```
function triple(value: number | string){
    if(typeof value === "string"){
        return value.repeat(3);
    }
    return value*3
}
```

---

## Truthiness Guards

**Truthiness Type Guards** involve checking a value for being truthy or falsy before working with it.

This is helpful in avoiding errors when values might be null or undefined.

```
const printLetters = (word: string | null) => {
    if(!word){
        //if word is null, don't loop over it
        console.log('No word has provided.');
    } else {
        //Only loop if word exists/is truthy
        name.forEach(letter => console.log(letter));
    }
}
```

function signatrue is the same as:

```
const printLetters = (word?: string) => {}
```

**DOM example**

Can look at the context

```
const el = document.getElementById("idk");
if(el){
    // el inferred as HTMLElement
}else {
    // el inferred as null
}
```

**Important note**

The first check does not conclusively say `word` must be a valid string, all that it says it's that is truthy

- Empty string is still a string but it is falsy.

In this case TS in the `else` block cannot say for sure that `word` is not a string

```
const printLetters = (word?: string) => {
    if(word){
        // word: string
        for(let char of word){
            console.log(char);
        }
    }else {
        // word: string | undefined
        console.log("YOU DID NOT PASS IN A WORD!");
    }
}
```

---

## Equality Narrowing

**equality Type Guards** involve comparing types to each other before doing certain operations with values.

By checking two values against one another, we can be sure they're both the same before working with them in a type-specific way.

```
const someFunc = (x: string | boolean, y: string | number) => {
    if (x === y){
        // x and y are strings in this case
        x.toUpperCase();
        y.toLowerCase();
    } else {
        console.log(x);
        console.log(y);
    }
}
```

---

## Narrowing With The In Operator

**in** Operator Narrowing

Javascript's **in** operator helps check if a certain property exists in an object.

This means we can use it to check if a value exists in an object, according to its type alias or alieases, before working with it.

```
type Cat = { meow: () => void};
type Dog = { bark: () => void};

const talk = (creature: Cat | Dog) => {
    if("meow" in creature) {
        console.log(creature.meow());
    } else {
        console.log(creature.bark());
    }
}

const kitty: Cat = {meow: () => 'MEOWW'};
talk(kitty); // MEOWW
```

**Example**

```
interface Movie {
    title: string,
    duration: number
}

interface TVShow {
    title: string,
    numEpisodes: number,
    episodeDuration: number
}

function getRuntime(media: Movie | TVShow){
    if("numEpisode" in media){
        return media.numEpisodes * media.episodeDuration;
    }
    return media.duration;
}

console.log(getRuntime({ title: "Amadeus", duration: 140 }))

console.log(getRuntime({ title: "Spongebob", numEpisodes: 80, episodeDuration: 30 }))
```

---

## Instanceof Narrowing

**instanceof** is a Javascript operator that allows us to check if one thing is an instance of another (remember prototypes?).

This can help us narrow types when working with things like classes.

```
const printFullDate(date: Date | string){
    if (date instanceof Date){
        return date.toUTCString();
    } else {
        return new Date(string).toUTCString();
    }
}
```

It will work for Classes, arrays, dates etc (anything with **new** keyword)

```
new Array() // same as
[]
```

```
[1,2,3] instanceof Array // true
[1,2,3] instanceof Date //false
```

**Example**

```
function printFullDate(date: string | Date){
    if(date instanceof Date){
        console.log(date.toUTCString());
    } else {
        console.log(new Date(date).toUTCString())
    }
}
```

Is entity instantiated from `User` or a `Company`

```
class User {
    constructor(public username: string){};
}

class Company {
    constructor(public name: string){}
}

function printName(entity: User | Company){
    if(entity instanceof User){
        entity // entity: User
    } else {
        entity // entity:  Company
    }
}
```

---

## Type Predicates

Typescript allows us to write custom functions that can narrow the type of a value. These functions have a very special return type called a type predicate.

A predicate takes the form **parameterName is Type**.

```
//": pet is dog --> type predicate!"
const isCat(pet: Cat | Dog): pet is Dog {
    return (pet as Dog).bark !== undefined;
}

let pet = getAnimal();
//pet gets passed to isCat above to narrow type
if(isCat(pet)){
    pet.meow();
} else {
    pet.bark();
}
```

**Example**

```
interface Cat {
    name: string;
    numLives: number;
}

interface Dog {
    name: string;
    breed: string;
}

function isCat(animal: Cat | Dog): animal is Cat {
    return (animal as Cat).numLives !== undefined
}

function makeNoise(animal: Cat | Dog): string {
    if(isCat(animal)){
        return "Meow"
    } else {
        // animal is Dog
    }
}
```

If we are narrowing the type all the type and try to determine is something is a user, admin etc we can create these special functions

---
