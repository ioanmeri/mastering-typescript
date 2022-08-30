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
