# Type Annotation Basics

**Primitive Types**

- Number
- String
- Boolean
- Null
- Undefined
- Void
- **Any**
- **Never**
- **Unknown**

**Object Types**

- Object
- Array
- Function
- **Tuple**
- **Enum**
- **Others!**

## Compiling TypeScript

```
tsc variables.ts
```

- a new file is created `variables.js`

## Type Inference

Type Inference refers to the Typescript compiler's ability to infer types from certain values in your code.

Typescript can remember a value's type even if you didn't provide a type annotation, and it will enforce that type moving forward.

## Any

'any' is an escape hatch! It turns off type checking for this variable so you can do your thing.

NOTE: it sort of defeats the purpose of TS and types, so use it sparingly!

## Delayed Initialization & Implicit Any

```
const movies = ["Arrival", "The Thing", "Aliens", "Amadeus"]
let foundMovie: string;
for(let movie of movies){
  if(movie === "Amadeus"){
    foundMovie = "Amadeus";
  }
}
```

if the annotation is not added, TS will infer the type to **any**

---
