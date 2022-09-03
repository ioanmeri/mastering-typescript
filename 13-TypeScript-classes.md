# TypeScript Classes

## Annotating Classes in TypeScript

For properties, we need to declare the type as well.

```
class Player {
  first: string;
  last: string;
  constructor(first: string, last: string) {
    this.first = first;
    this.last = last;
  }
}

const elton = new Player("Elton", "Steele");

```

---

## Annotating Fields

We can rely often on inferring the type

```
class Player {
  score = 0;
}

```

can also add the annotation to be clear:

```
class Player {
  score: number = 0;
}

```

---

## Readonly modifier

Unique to TypeScript, does not exist in JS.

```
class Player {
  readonly first: string;
  readonly last: string;

  constructor(first: string, last: string) {
    this.first = first;
    this.last = last;
  }
}

const elton = new Player("Elton", "Steele");
```

Then changing the first would give an error, it's read only:

```
elton.first = "elton"
```

---

## The public modifier

Exclusive to TypeScript, don't exist in JS.

In JavaScript, every single property and method is considered public.

Can modify them outside of the class.

Don't really need the public modifier, but it's used to show to other developers that a property is changeable - accessible - writeable outside of the class.

```
class Player {
  public readonly first: string;
  public readonly last: string;
  public score: number = 0;
}
```

Used for clarity sake, to be explicit.

> Public - visibility

> readonly - whether you can actually **write** to the property

---

## The private modifier

We can put `private` in front of any property or method and that will tell TypeScript that this property or method is only accessible or usable, **inside the class**.

```
class Player {
  private score: number = 0;
}
```

```
elton.score // TS will give an error, only accessible within that class
```

This is different than the `#score` from JavaScript

It will give an error because

- '#score' is declared but its value is never read. Private identifiers are only available when targeting ECMAScript 2015 and higher. (not supported default es5)

but if the target version is "es2015", it works and outside of the class we have:

```
elton.#score; // '#score' is not accessible outside class 'Player' because it has a private identifier.
```

Can use the private modifier:

```
class Player {
  private score: number = 0;
}
```

but cannot use both:

```
class Player {
  private #score: number = 0; // An accessibility modifier cannot be used with a private identifier.
}
```

> The hash symbol from JS, provides protection not just before the compilation but actually when the code is running as well.

If I have a private method, TS will give an error but it will actually compile to JS and run

```
class Player {
  private secretMethod(): void {
    console.log("SECRET METHOD!!");
  }
}

elton.secretMethod();
```

---

## Parameter Properties Shorthand

**From**:

```
class Player {
  public readonly first: string;
  public readonly last: string;

  constructor(first: string, last: string) {
    this.first = first;
    this.last = last;
  }
}
```

**To**:

```
class Player {
  constructor(public first: string, public last: string) {}
}
```

- don't have to initialize parameters
- don't have to set parameters separately

---

## Getters and Setters

### Getters

```
class Player {
  constructor(public first: string, public last: string) {}

  get fullName(): string {
    return `${this.first} ${this.last}`;
  }
}
```

Anytime TS seas a property name that does not have a setter and only has a getter, TS will make it **read-only**

### Setters

```
class Player {
  constructor(
    private _score: number
  ) {}

  get score(): number {
    return this._score;
  }

  set score(newScore: number) {
    if (newScore < 0) {
      throw new Error("Score cannot be negative!");
    }
    this._score = newScore;
  }
}

this.score = 99 // this will update _score
```

> In TS, setters cannot have a return type

---

## The protected modifier

Protected comes into play when we work with inheritance

We want a (not public) property to be accessible from a child class as well

**Base class**

```
class Player {
  constructor(
    protected _score: number
  ) {}
}
```

**Super class**

```
class SuperPlayer extends Player {
  public isAdmin: boolean = true;
  maxScore() {
    this._score = 999999;
  }
}
```

---
