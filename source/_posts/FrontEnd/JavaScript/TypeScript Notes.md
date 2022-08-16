---
title: TypeScript Notes
date: 2022-07-12 15:05:45
tags:
---

## Types

- string
- number

  这里和 JavaScript 一样没有`int`或者`float`

- boolean
- Arrays

  - 数字类型，可以使用`number[]`，`Array<numer>`
  - 字符串类型，可以使用`string[]`，`Array<string>`

- any

  可适用于任何类型

- `noImplicitAny`<font color="red">待定</font>

赋值时，可以不需要声明类型，typescript 会自动识别类型。然而如果改变另一个类型，typescript 会报错。比如：

```TypeScript
let str = "hello";
str = 100; //error: Type 'number' is not assignable to type 'string'
```

- Function

```TypeScript
function greet(name:string){
    console.log(`Hello ${name.toUpperCase()}!!`);
}

//通常不需要声明类型，因为ts会自动判断
function getFavoriteNumer():numer{
    return 26;
}
```

### 联合类型

```TypeScript
function welcomePeople(x: string[] | string){
    if(Array.isArray(x)){
        console.log(`Hello, ${x.join('and')}`)
    }else{
        console.log(`Weolcome lone traveler ${x}`)
    }
}
```

### Type Aliases and Interfaces（类型别名和接口）

`Type Aliases`一般用于包含多个属性的对象，就可以封装一个 type，然后赋值到另一个值上。

```TypeScript
type Point = {
    x:numer;
    y:number
}

function printCoord(pt: Point){
    ...
}
```

`Interfaces`和上面类似，但它们还是有区别，看下面的 🌰：

- Interface

  ```typescript
  interface Animal {
    name: string;
  }
  interface Bear extends Animal {
    honey: boolean;
  }
  const bear = getBear();
  bear.name;
  bear.honey;
  ```

- Type

  ```typescript
  type Animal = {
    name: string;
  };
  type Bear = Animal & {
    honey: boolean;
  };
  ```

- Type Assertions（类型断言）
