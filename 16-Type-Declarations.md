# Type Declarations

Working With 3rd Party Code

## Introducing Type Declarations

Special files in TS that end in `.d.ts` that serve a very special purpose. In a `.d.ts` we would find no implementation details, no code but instead we find files that contain:

**only type information**

declarations of types which TS can lookup and use to understand and enforce type rules on our code.

**Example**

When I write `console.log` that method exist in an **Console interface** of `lib.dom.d.ts` file

---

## Working with Axios Types

`Axios get` method is a **generic** that accepts a type and whatever type we provide will be passed to axios response (of the same generic type).

We can declare an interface and pass it to get so we can cast the response with pre-defined properties

```
interface User {
  id: number;
  name: string;
  username: string;
  email: string;
  address: {
    street: string;
    suite: string;
    city: string;
    zipcode: string;
    geo: {
      lat: string;
      lon: string;
    };
  };
  phone: string;
  website: string;
  company: {
    name: string;
    catchPhrase: string;
    bs: string;
  };
}

axios
  .get<User>("https://jsonplaceholder.typicode.com/users/1")
  .then((res) => {
    console.log("WOO!!!");
    const { data } = res;
    printUser(res.data);
  })
  .catch((e) => {
    console.log("ERROR!", e);
  });

function printUser(user: User) {
  console.log(user.name);
  console.log(user.email);
  console.log(user.phone);
}

```
