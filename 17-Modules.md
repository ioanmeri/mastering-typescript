# Modules

The different ways of sharing code between files (commonjs, es modules).

## Working Without Modules

The JavaScript specification declares that any JavaScript files without an `export` or top-level `await` should be considered a script and not a module.

Inside a **script** file variables and types are declared to be in the **shared global scope**

---

## Using TypeScript Modules

Even if there is an `export` in one file then that it is considered a **es module** and have to manually import / export any functionality I want to share.

We can write **es module syntax** (import / export) and TypeScript will (not complain) be able to compile this code to some other module syntax - **commonjs modules** (require, module.exports)

---
