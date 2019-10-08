------

1. 输出是什么？ （考察知识点，基本包装类型，==和===的区别）

```javascript
let a = 3
let b = new Number(3)
let c = 3

console.log(a == b)
console.log(a === b)
console.log(b === c)
```

+ A: `true` `false` `true`
+ B: `false` `false` `true`
+ C: `true` `false` `false`
+ D: `false` `true` `true`

##### 答案 C

`new Number()` 是一个内建的函数构造器(基本包装类型，是一个对象)。

当我们使用 `==` 操作符时，只会检查两者是否拥有相同的 **值** 。因为它们的值都是 `3`，因此返回 `true`。

然后，当我们使用 `===` 操作符时，两者的**值和类型** 都应该是相同的。`new Number()` 是一个对象而不是 number，因此返回 `false`。

------

2. 输出是什么？ （考察知识点，常规函数和箭头函数this指向的区别）

```javascript
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2
  },
  perimeter: () => 2 * Math.PI * this.radius
}

shape.diameter()
shape.perimeter()
```

+ A: `20` and `62.83185307179586`
+ B: `20` and `NaN`
+ C: `20` and `63`
+ D: `NaN` and `63`

##### 答案 B

常规函数中的this谁调用就指向谁，箭头函数，`this` 关键字指向的是它当前周围作用域（简单来说是包含箭头函数的常规函数，如果没有常规函数的话就是全局对象）。

所以当我们调用 `perimeter` 时，`this` 不是指向 `shape` 对象，而是它的周围作用域（在例子中是 `window`）。 在 `window` 中没有 `radius` 这个属性，因此返回 `undefined`。 `undeifined ` 参与运算之后返回NaN

-----

3. 一些知识点总结（非数值的数值转换）

+ 主要函数: `Number() parseInt() parseFloat()  `
+ 转换规则: 
  + Boolean类型 true返回1 false返回0   
  + Number 类型 直接返回
  + null类型 返回0   
  + undefined 返回 NaN
  + String 类型
    +  ‘123’只包括数字（包含正负号），直接转换。
    + 十六进制 转换为10进制数。字符串空，返回0。
    + 以上不满足，则不能转换，直接返回NaN。  

----

4. 哪一个是无效的？ （考察知识点，字面量和`.`取值的区别）

```javascript
const bird = {
  size: 'small'
}

const mouse = {
  name: 'Mickey',
  small: true
}
```

- A: `mouse.bird.size`
- B: `mouse[bird.size]`
- C: `mouse[bird["size"]]`
- D: All of them are valid

##### 答案 A

[] 当我们使用括号语法时（[]), []里面的内容先读取，进行计算。因此，mouse[bird.size] 先计算括号里面的值 。

当我们使用 `.`语法时，顺序计算。 因此，mouse.bird.size 先计算mouse.bird，再计算.size 。因此会报错。

---

5. 输出是什么？（考察知识点，类和静态方法的使用）

```javascript
class Chameleon {
  static colorChange(newColor) {
    this.newColor = newColor
    return this.newColor
  }

  constructor({ newColor = 'green' } = {}) {
    this.newColor = newColor
  }
}

const freddie = new Chameleon({ newColor: 'purple' })
freddie.colorChange('orange')
```

- A: `orange`
- B: `purple`
- C: `green`
- D: `TypeError`

##### 答案: D

`colorChange` 是一个静态方法。静态方法被设计为只能被创建它们的构造器使用（也就是 `Chameleon`），并且不能传递给实例。因为 `freddie` 是一个实例，静态方法不能被实例使用，因此抛出了 `TypeError` 错误。 

---

6. 当我们这么做时，会发生什么？ （考察知识点，JS对象）

```javascript
function bark() {
  console.log('Woof!')
}

bark.animal = 'dog'
```

- A: 正常运行!
- B: `SyntaxError` 你不能通过这种方式给函数增加属性。
- C: `undefined`
- D: `ReferenceError`

#####答案: A

这在 JavaScript 中是可以的，因为函数是对象！（除了基本类型之外其他都是对象,都可以拥有属性并且调用）！

---

7. 事件传播的三个阶段是什么？ （考察知识点，事件传播的一些定义理解）

- A: Target > Capturing > Bubbling
- B: Bubbling > Target > Capturing
- C: Target > Bubbling > Capturing
- D: Capturing > Target > Bubbling

#####答案: D

在**捕获**（capturing）阶段中，事件从祖先元素向下传播到目标元素。当事件达到**目标**（target）元素后，**冒泡**（bubbling）才开始。

![1566614452544](C:\Users\HP\AppData\Local\Temp\1566614452544.png)

##### 待补充知识点

事件捕获

事件执行（target）

事件冒泡

---

8. 输出是什么？（考察知识点，eval() 函数基本知识）

```javascript
const sum = eval('10*10+5')
```

- A: `105`
- B: `"105"`
- C: `TypeError`
- D: `"10*10+5"`

#####答案: A

eval() 函数可计算某个字符串，并执行其中的的 JavaScript 代码。

eval(string)，通过计算 string 得到的值（如果有的话）。 

---

9. 输出是什么？ （考察知识点， `'use strict'` 不意外声明全局变量）

```javascript
function getAge() {
  'use strict'
  age = 21
  console.log(age)
}

getAge()
```

- A: `21`
- B: `undefined`
- C: `ReferenceError`
- D: `TypeError`

##### 答案: C

 `'use strict'` 不意外声明全局变量, 它将抛出一个引用错误。 

##### 补充知识点: 

ReferenceError和TypeError的区别:

+ ReferenceError：引用错误，即在作用域中没有找到该变量 

```javascript
console.log(a);    // ReferenceError
```

+ TypeError：类型错误，在作用域中已经声明变量并且找到，但是没有找到确切定义或者引用 

```js
foo(); // TypeError
bar(); // ReferenceError
var foo = function bar() {
    // ...
};
```

当在作用域中找到了这个变量引用，然后你让这个变量去做他力所不能及的事情的时候，比如说引用它一个不存在的属性，比如说将非函数的变量用作函数引用，这个时候JavaScript引擎就会抛出TypeError。 

```javascript
var a;
console.log(a.age);  //TypeError
```

总结：一般ReferenceError是没找到变量，一般TypeError是变量找到了，但是引用属性的时候找不到属性。

---

10. cool_secret 可访问多长时间？（考察知识点，sessionStorage和localStorage的区别）

```javascript
sessionStorage.setItem('cool_secret', 123)
```

- A: 永远，数据不会丢失。
- B: 当用户关掉标签页时。
- C: 当用户关掉整个浏览器，而不只是关掉标签页。
- D: 当用户关闭电脑时。

##### 答案: B

关闭 **tab 标签页** 后，`sessionStorage` 存储的数据才会删除。

如果使用 `localStorage`，那么数据将永远在那里，除非调用了 `localStorage.clear()`。

---

11. 输出是什么？ 

```javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const member = new Person("Lydia", "Hallie");
Person.getFullName = function () {
  return `${this.firstName} ${this.lastName}`;
}

console.log(member.getFullName());
```

- A: `TypeError`
- B: `SyntaxError`
- C: `Lydia Hallie`
- D: `undefined` `undefined`

##### 答案: A

