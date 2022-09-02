# Mini Project: The DOM, Type Assertions, and More!

## Initializing a new project

1. Create `tsconfig.json` file

```
tsc --init
```

2. Create project directories

```
mkdir src dist
```

3. Create `index.ts` file

```
touch src/index.ts
```

4. Change output directory of `jsconfig.json`

From:

```
"outDir": "./"
```

To:

```
"./dist"
```

5. Only include _src_ directory

Add in `jsconfig.json`

```
"include": ["src"]
```

6. Start watch mode

```
tsc -w
```

7. Create `src/index.html` and add script tag

```
<script src="dist/index.js"></script>

```

8. Add live server (all TS settings are complete)

```
npm init -y
```

and

```
npm install lite-server
```

9. Add start command

In scripts add:

```
"start": "lite-server"
```

which has auto refresh capability

10. Start live server and TS watch mode

```
tsc -w
```

and

```
npm start
```

---

## The Lib Compiler Option

the default lib property (which is commented out) includes the `DOM`

If the lib option is turned on empty:

```
"lib": []
```

then TS doesn't know about `document`, empty lib removes the DOM types, can add it back manually with `DOM`

### ES2021

`ES2021` library can be included in the lib arrays to support es2021 functions (even though the target is `es5`)

or can just say:

```
"target": "es2021"
```

---

## TypeScript's Non-Null Assertion Operator

If before runtime a `const btn` is declared like this:

```
const btn = document.getElementById("btn");
```

the btn type is `HTMLElement | null` because TS doesn't know before hand if the selected element is

- button (HTMLButtonElement)
- h1
- image
- p
- etc.
- null

Then if I try to add an event listener:

```
btn.addEventListener("click")
```

TS will complain that **Object is possibly null**

There are 2 solutions:

- the question mark operator (btn?.addEventListener)
- TS approach

**Non-Null Assertion Operator**

This is guaranteed btn not to be null, so type is an `HTMLElement`

```
const btn = btn.addEventListener("click")!;
```

---

## Type Assertions

Sometimes you might have more specific information about a value's type, and you want to make sure Typescript knows it too.

You can assert a value's type by using the **'as'** keyword, followed by the specific type you want to assert.

```
//Typescript infers a type of HTMLElement
const myPic = document.querySelector("profile-image");

//But we know a more specific type, so let's assert it!
const myPic = document.querySelector("profile-image") as HTMLImageElement;
```

**Only in that context mystery is a string, otherwise it's unknown as declared**

```
const mystery: unknown = "Hello World!!!";

const numChars = (mystery as string).length
```

**Another example**

```
const input = document.getElementById("todoinput")! as HTMLInputElement;
```

same as

```
//The same assertion with:
(<HTMLInputElement>input).value
```

---
