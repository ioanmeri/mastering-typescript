# The TypeScript Compiler

## Configuring TypeScript

```
tsc --init
```

This creates a `tsconfig.json` file

Running `tsc index.ts` it creates the `index.js` file

## Watch mode

Listen for changes anytime we modify the `index.ts` file

```
tsc -w index.ts
```

or longer version:

```
tsc --watch index.ts
```

## Working With Multiple Files

Running

```
tsc
```

it will compile any `.ts` files that it comes across

and the same goes for the watch mode

```
tsc -w
```

## The Files compiler options

it's outside of the compiler option in the `tsconfig.json`, it's top level option

We list out all the files with want TS to include in an array

Great to list out **manually** the files that you want to TS to compile
