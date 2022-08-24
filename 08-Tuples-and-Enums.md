# Tuples and Enums

## Tuples

Tuples are a special type exclusive to TypeScript (they don't exist in JS)

Tuples are arrays of fixed lengths and ordered with specific types - like super rigid arrays.

```
// Creating a Tuple with its type definition
let myTuple: [number, string];

//CAN assign it values per its specs
myTuple = [10, 'Typescript is fun!']

//CAN'T assign it values of a dif structure
myTuple = ['Typescript is fun!', 10]
```

```
const color: [number, number, number] = [255, 0, 255];
```

```
type HTTPResponse = [number, string];

const goodRes: HTTPResponse = [200, "OK"];
// goodRes[0] = "200" //error
goodRes.push(123) // if push after the tuple is created, TS will let it go
goodRes.pop()
goodRes.pop()
goodRes.pop()
```

```
const responses: HTTPResponse[] = [[404, "Not Found"], [200, "OK"]]
```

---

## Enums

Enums allow us to define a **set of named constants**. We can give these constants numeric or string values.

There's quite a few options when it comes to enums!

```
//Number Enums
enum Responses {
  no, //1
  yes, //2
  maybe, //3
}

enum Responses {
  no = 2, //2
  yes, //3
  maybe, //4
}

enum Responses {
  no = 2, //2
  yes = 10, //10
  maybe = 24, //24
}

//String Enums
enum Responses {
  no = 'No',
  yes = 'Yes',
  maybe = 'Maybe'
}

//Heterogenous Enums
enum Responses {
  no = 0,
  yes = 1,
  maybe = 'Maybe'
}
```

```
enum OrderStatus {
  PENDING,
  SHIPPED,
  DELIVERED,
  RETURNED
}

const myStatus = OrderStatus.DELIVERED;

function isDelivered(status: OrderStatus){
  return status === OrderStatus.DELIVERED
}

isDelivered(OrderStatus.RETURNED)
```

**String enum**

```
enum ArrowKeys {
  UP = "up",
  DOWN = "down",
  LEFT = "left",
  RIGHT = "right"
}
```

## Behind the scenes

**Underline JS code that results from the TS enum**

**From TS**

```
enum OrderStatus {
  PENDING,
  SHIPPED,
  DELIVERED,
  RETURNED
}
```

**To JS**

```
**use strict*;
var OrderStatus;
(function(OrderSTatus){
  OrderStatus[OrderStatus["PENDING"] = 0] = "PENDING";
  OrderStatus[OrderStatus["SHIPPED"] = 1] = "SHIPPED";
  OrderStatus[OrderStatus["DELIVERED"] = 2] = "DELIVERED";
  OrderStatus[OrderStatus["RETURNED"] = 3] = "RETURNED";
})(OrderStatus || (OrderStatus = {}))
```

if enum is turned to const

```
enum OrderStatus {
  PENDING,
  SHIPPED,
  DELIVERED,
  RETURNED
}
```

then it replaces every value referenced from order status with the underlying number.

everything related to OrderStatus is stripped out

---
