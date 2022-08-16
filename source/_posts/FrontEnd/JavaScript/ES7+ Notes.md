---
title: ES7+ Notes
date: 2022-06-24 16:54:32
tags: JavaScript
categories: FrontEnd
---

参考网址：

- [2022 年了，这些 ES7-ES12 的知识点你都掌握了嘛？](https://mp.weixin.qq.com/s/XyU_GuhNqxAh2j8PIpe9Mw)

## ES7

- `Array.propertype.includes()`

  判断一个数组是否包含一个指定的值，返回*boolean*，能识别`NaN`，indexOf 不能识别

- 幂运算符 `**`

  相当于`Math.pow()`

  ```JavaScript
  2 ** 3; //8
  ```

## ES8

- `Object.values()`

  返回一个数组：参数对象自身的**（不含继承）所有可枚举属性的值**

- `Object.entries()`

  返回一个数组：参数对象自身的**（不含继承）所有可枚举属性的键值对数组**

  ```JavaScript
  const obj = {
    name: "fency",
    age: 18,
  };
  Object.entries(obj); //[['name','fency'],['age',18]]
  ```

- `Object.getOwnPropertyDescriptors()`

  获取一个对象的所有自身属性的描述符，比如`value`,`writable`,`enumerable`,`configurable`

- `String.prototype.padStart(targetLength[,padString])`

  把`padString`填充到字符串头部，返回新的字符串

  - `targetLength`是指当前字符串需要填充到的目标长度，如果这个数值**小于**当前字符串的长度，则返回**当前字符串本身**
  - `padString`填充字符串，如果填充后的字符串超过了目标长度，则会截取最左则的部分，默认值为" "

  ```javascript
  "abc".padStart(6); //"   abc"
  "abc".padStart(1, "h"); //"abc"
  "abc".padStart(6, "123456"); //"123abc"
  ```

  常见的场景：月份<10，前面加上 0，`padStart(2, '0')`

- `String.prototype.padEnd(targetLength[,padString])`

  （同上）

- `尾逗号`

  参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Trailing_commas

- `async/await`

## ES9

- `Object Rest & Spread`

  Spread（展开）的用法：

  > ⚠️：属性的值是一个对象的话，该对象的引用会被拷贝，而不是生成一个新的对象。

  ```javascript
  const input = {
    a: 1,
    b: 2,
    c: 3,
  };

  const output = {
    ...input,
    c: 4,
  };

  console.log(output); // {a: 1, b: 2, c: 4}
  ```

  Rest 的用法：

  ```javascript
  const input = {
    a: 1,
    b: 2,
    c: 3,
  };

  let { a, ...rest } = input;

  console.log(a, rest); // 1 {b: 2, c: 3}
  ```

- `for await of`

  异步迭代器，循环等待每个 Promise 对象变为 resolved 状态才进入下一步

  ```javascript
  function TimeOut(time) {
    return new Promise(function (resolve, reject) {
      setTimeout(function () {
        resolve(time);
      }, time);
    });
  }

  async function test() {
    let arr = [TimeOut(2000), TimeOut(1000), TimeOut(3000)];
    for await (let item of arr) {
      console.log(Date.now(), item);
    }
  }
  test();
  // 1560092345730 2000
  // 1560092345730 1000
  // 1560092346336 3000
  ```

- `Promise.prototype.finally()`

- `String扩展`

## ES10

- `Object.fromEntries()`

  把键值对列表转换为一个对象，和`Object.entries()`相对的

  ```javascript
  Object.fromEntries([
    ["foo", 1],
    ["bar", 2],
  ]);
  // {foo: 1, bar: 2}
  ```

  e1：可以把`Map`转为`Object`

  ```javascript
  const map = new Map();
  map.set("name", "jimmy");
  map.set("age", 18);
  console.log(map); // {'name' => 'jimmy', 'age' => 18}

  const obj = Object.fromEntries(map);
  console.log(obj);
  // {name: "jimmy", age: 18}
  ```

  e2：过滤的简洁方法，比如：

  ```javascript
  const course = {    math: 80,    english: 85,    chinese: 90}const res = Object.entries(course).filter(([key, val]) => val > 80)console.log(res) // [ [ 'english', 85 ], [ 'chinese', 90 ] ]console.log(Object.fromEntries(res)) // { english: 85, chinese: 90 }
  ```

  e3：url 的 search 参数转换

  ```javascript
  // let url = "https://www.baidu.com?name=jimmy&age=18&height=1.88"// queryString 为 window.location.searchconst queryString = "?name=jimmy&age=18&height=1.88";const queryParams = new URLSearchParams(queryString);const paramObj = Object.fromEntries(queryParams);console.log(paramObj); // { name: 'jimmy', age: '18', height: '1.88' }
  ```

- `Array.prototype.flat()`

  拉平数组

- `Array.prototype.flatMap()`

  使用映射函数映射每个元素，然后将结果压缩成一个新数组

  ```javascript
  var new_array = arr.flatMap(function callback(currentValue[, index[, array]]) {    // 返回新数组的元素}[, thisArg])
  ```

- `String.prototype.trimStart()`

  删除字符串的开头空格，也可以用`trimLeft()`

  ```javascript
  let str = '   foo  'console.log(str.length) // 8str = str.trimStart() // 或str.trimLeft()console.log(str.length) // 5
  ```

- `String.prototype.trimEnd()`

  删除字符串的右端空白，也可以用`trimRight()`

- `可选的Catch Binding`

  ```javascript
  try {
    console.log("Foobar");
  } catch {
    console.error("Bar");
  }
  ```

  e1：**验证参数是否为 json 格式**

  ```javascript
  const validJSON = json => {    try {        JSON.parse(json)        return true    } catch {        return false    }}
  ```

- `Symbol.prototype.description`

  可以读取属性，如果没有描述符，将会返回`undefined`

  ```javascript
  const name = Symbol("es")name.toString(); //Symbol(es)name.description; //es
  ```

- `JSON.stringify()`增强能力

  修复了一些超出范围的 Unicode 展示错误的问题

- 修订`Function.prototype.toString()`

  以前函数的 toString 方法来自`Object.prototype.toString()`，现在的`Function.prototype.toString() `方法返回一个表示当前函数源代码的字符串。以前只会返回这个函数，不包含注释、空格等。

  ```javascript
  function foo() {    // es10新特性    console.log('imooc')}console.log(foo.toString()) // 打印如下// function foo() {//  // es10新特性//  console.log("imooc");// }
  ```

  ## ES11

  - 空值合并运算符`??`（Nullish coalescing Operator）

    `??`是一个逻辑操作符，当左侧的操作数为 `null`或者`undefined`时，返回其右侧操作数，否则返回左侧操作数

    ```javascript
    const foo = undefined ?? "foo"const bar = null ?? "bar"console.log(foo) // fooconsole.log(bar) // bar
    ```

    对于需要判断`undefined`或者`null`很有用

  - 可选链`?.`

    允许读取位于连接对象链深处的属性的值，而不必明确验证链中的每个引用是否有效，如果读取不到，会返回`undefined`。与函数调用一起使用时，如果给定的函数不存在，则返回 `undefined`

    ```javascript
    const user = {    address: {        street: 'xx街道',        getNum() {            return '80号'        }    }}const street2 = user?.address?.streetconst num2 = user?.address?.getNum?.()console.log(street2, num2)// 与 ?? 一起使用let customer = {  name: "jimmy",  details: { age: 18 }};let customerCity = customer?.city ?? "成都";console.log(customerCity); // "成都"
    ```

- `globalThis`

  提供了一个标准的方式来获取不同环境下的全局 `this` 对象（也就是全局对象自身）。不像 `window` 或者 `self` 这些属性，它确保可以在有无窗口的各种环境下正常工作。所以，你可以安心的使用 `globalThis`，不必担心它的运行环境。

- `BigInt`

  任意大的整数

- `String.prototype.matchAll()`

  返回一个包含所有匹配正则表达式的结果及分组捕获组的迭代器

  ```javascript
  const regexp = /t(e)(st(\d?))/g;
  const str = "test1test2";
  const array = [...str.matchAll(regexp)];
  console.log(array[0]); // ["test1", "e", "st1", "1"]console.log(array[1]); // ["test2", "e", "st2", "2"]
  ```

- `Promise.allSettled()`

  之前的`Promise.all()`可以并发执行异步任务的，但它有个缺点，其中某一个任务出现 reject，所有的任务都会挂掉，直接进入 reject 状态。所以需要`allSettled()`来处理，不论某一个任务异常，都会返回对应的状态。

  ```javascript
  // Promise.allSettled 不管有没有错误，三个的状态都会返回Promise.allSettled([promise1(), promise2(), promise3()])  .then((res) => {    console.log(res);      // 打印结果     // [    //    {status: 'fulfilled', value: 'promise1'},     //    {status: 'fulfilled',value: 'promise2'},    //    {status: 'rejected', reason: 'error promise3 '}    // ]  })  .catch((error) => {    console.log("error", error);   });
  ```

- `Dynamic Import`(按需 import)

  `import()`可以在需要的时候，加载某个模块

  ```javascript
  button.addEventListener("click", (event) => {
    import("./dialogBox.js")
      .then((dialogBox) => {
        dialogBox.open();
      })
      .catch((error) => {
        /* Error handling */
      });
  });
  ```

## ES12

- 逻辑运算符和赋值表达式

  - `&&=`

  ```javascript
  //x &&= y 相当于 x && (x=y)
  ```

  - `||=`

  ```javascript
  // x||=y 相当于x || (x=y)
  ```

  - `??=`(仅针对`null`或`undefined`)

  ```javascript
  // x??=y 相当于x ?? (x=y)
  ```

- `String.prototye.replaceAll()`

- 数字分隔符`_`

- `Promise.any`

## ES13

- class

  - 之前如果需要私有变量，比如说`_name`，加上`_`标志为私有变量，不让外部可访问到，但事实上却可以访问到，看下面的 🌰：

  ```JavaScript
  class User{
    constructor(){
      this._name = "nancy"
    }
  }

  const user = new User()
  user._name; //
  ```
