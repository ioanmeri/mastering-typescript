# Javascript classes

- constructors
- class fields
- getters and setters
- private # fields
- static fields / methods
- inheritance
- supe

## The Class Keyword

Classes are templates for creating objects in Javascript. They contain a few different important pieces which allow for creation and extension of customized (and nicely organized) objects.

## Constructor

```
//Our blueprint for a person
class Person {
  constructor(name, age){
    this.name = name;
    this.age = age;
  }
  greet(){
    return `Hello ${this.name}!`;
  }
}

//Using our blueprint to make a real person
const jimmy new Person("Jimmy", 25);

//Using some methods that our new object has
//based on the blueprints
jimmy.greet(); //Hello Jimmy!
```

---

## Class fields

```
class Player {
  score = 0;
  numLives = 10;
  constructor(){

  }
  loseLife() {
    this.numLives -= 1;
  }
```

---

## Private Fields

Any property that starts with a hash tells JavaScript that this property should be usable only inside of this class.

```
class Player {
  #score = 0;
  constructor(){
    ...
  }
  #secret() {
    console.log("SECRET!!");
  }
}

player1.#score // syntax error, not allowed // not available outside the class;
```

---

## Getters

Getters expose a value publicly

```
class Player {
  #score = 0;
  constructor(first, last) {
    this.first = first;
    this.last = last;
  }

  get fullName() {
    return `${this.first} ${this.last}`;
  }

  get score() {
    return this.#score;
  }
}

const player1 = new Player("blue", "steele");

console.log(player1.fullName);
```

---

## Setters

```
class Player {
  #score = 0;

  set score(newScore) {
    if (newScore < 0) {
      throw new Error("Score must be positive!");
    }
    this.#score = newScore;
  }
}

player1.score = 324;
```

---

## Static methods / properties

If we put it in front of a property or method, that tells JS that property or method exist on the class itself, but not in each individual instance

Allows us to group functionality in with the class that doesn't have anything to do with the particular instance but still maybe has to do with the class itself.

```
class Player {
  static description = "Player In Our Game";

  static randomPlayer(){
    return new Player("Andy", "Samberg");
  }
}
```

I can access it only through the class:

```
Player.description
Player.randomPlayer()
```

but not from the instances

---

## Extending Classes

Extending from a base or parent or super class. We have access to all the same functionality.

```
class AdminPlayer extends Player {
  isAdmin = true;
}
```

## Super keyword

When we don't have a constructor added on to the child class, JS automatically calls the constructor function of the parent class (as well as it founds one).

```
class AdminPlayer extends Player {
  isAdmin = true;
}

const admin = new AdminPlayer("admin", "mCadmin");
```

If we have another constructor in child class, only that will run

Super references the constructor of the super class:

```
class AdminPlayer extends Player {
  constructor(powers){
    this.powers = powers;
  }
  isAdmin = true;
}

const admin = new AdminPlayer("admin", "mCadmin");
```

**JS Example**

```

class Player {
  static description = "Player In Our Game";
  #score = 0;
  numLives = 10;
  constructor(first, last) {
    this.first = first;
    this.last = last;
    // this.#secret = 'valid as well';
  }
  static randomPlayer() {
    return new Player("Andy", "Samberg");
  }
  get fullName() {
    return `${this.first} ${this.last}`;
  }
  set fullName(newName) {
    const [first, last] = newName.split(" ");
    this.first = first;
    this.last = last;
  }

  get score() {
    return this.#score;
  }
  set score(newScore) {
    if (newScore < 0) {
      throw new Error("Score must be positive!");
    }
    this.#score = newScore;
  }

  getScore() {
    return this.#score;
  }
  updateScore(newScore) {
    this.#score = newScore;
  }
  taunt() {
    console.log("BOOYAH!");
  }
  loseLife() {
    this.numLives -= 1;
  }
  #secret() {
    console.log("SECRET!!");
  }
}

class AdminPlayer extends Player {
  constructor(first, last, powers) {
    super(first, last);
    this.powers = powers;
  }
  isAdmin = true;
}

const admin = new AdminPlayer("admin", "mCadmin", ["delete", "restore world"]);
console.log(admin);
```
