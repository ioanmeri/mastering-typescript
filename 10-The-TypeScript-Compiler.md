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

## Include, Exclude files

**Include** specifies an array of filenames or patterns to include in the program. These filenames are resolved relative to the directory containing the `tsconfig.json` file

```
{
  "include": ["src/**/*", "tests/**/*"]
}
```

`[]` if files options is specified, `**` otherwise

**Exclude** defaults to `node_modules`, if I add a custom exclude I have to add the `node_modules` as well

## Outdir option

Usually we compile all the ts files to js into a separate directory. A common name would be dist.

This can by done by adding this to compiler option:

```
"outDir": "./dist",
```

## Target option

It governs the output version that TS compiles into.

e.g. es6 supports arrow functions / const but es5 does not

## Strict

defaults to true
