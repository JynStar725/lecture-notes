## 声明变量的新姿势

---

在es6之前我们使用`var`来声明一个变量，但是有很多的弊端：

- 因为没有块级作用域，很容易声明全局变量
- 变量提升
- 可以重复声明

```javascript
var a = []
for (var i = 0, i< 10, i++) {
    a[i] = function () {
        console.log(i)
    }
}

a[6]() // 10
a[7]() // 10
a[8]() // 10
a[9]() // 10
```



## 有时候const比let更好

---

const和let唯一的区别是，const不可以更改，使用const的优点

- 更好的代码语义化，一眼就看到是常量
- Javascript编译器对const的优化比let的要好
- 所有的函数都应该设置常量



## 动态字符串

---

不要使用双引号，一律使用单引号或者反引号

```javascript
const a = 'foo'
const b = `${foo} bar`
```



## 解构赋值的骚操作

### 变量赋值

---

在用到数组成员对变量赋值时，尽可能使用解构赋值

```javascript
const arr = [1, 2, 3, 4]

const {first, second} = arr

console.log(first)  // 1
console.log(second) // 2
```



### 函数传对象

---

如果函数的参数是对象的成员，优先使用解构赋值

```javascript
// low
function getFullName(user) {
	const firstName = user.firstName
    const lastName = user.lastName
}

// good
funciton getFullName({firstName, lastName}) {
    ...
}

```

如果函数返回多个值，优先使用对象的解构赋值，而不是数组的解构赋值，这样便于以后添加返回值，以及更改返回值的顺序。**对象的解构赋值是根据key值进行匹配的**

```javascript
// low
function procssInput(input) {
    return [left, right, top, bottom]
}

// good
function processInput(input) {
    return {left, right, top, bottom}
}

// 好处
const {left, right} = processInput(input)
```



## 数组

### ...扩展运算符

---

使用扩展运算符`...`拷贝数组

```javascript
// cool
const arr = [1, 2, 3, 4]

const arrCopy = [...arr]
// 产生一个新的数组
console.log(arrCopy === arr) // false
```



### 不要提类数组

---

`Array.from()`方法，将类似数组（可迭代）的对象转为数组

```js
const foo = document.getElementByTagName('div')
const divArr = Array.from(foo)
```



不要把布尔值直接传入函数中

---

```js
// low
function divide(a, b, option = false) {
}

// good
function divide(a, b, {option = false} = {}) {
    
}
```



### 传参时试试设置默认值？

---

```js
// low
function handleThings(opts) {
  opts = opts || {}
}

// good
function handleThings(opts = {}) {
  // ...
}
```



## Object？Map！

### 简单的键值对优先Map

---

如果只是简单的key: value结构，建议优先使用Map，因为Map提供方便的遍历机制。

```js
let map = new Map(arr)
// 遍历key值
for (let key of map.keys()) {
  console.log(key)
}
// 遍历value值
for (let value of map.values()) {
  console.log(value)
}
// 遍历key和value值
for (let item of map.entries()) {
  console.log(item[0], item[1]);
}
```



## 编码规范

---

- 模块输出一个函数，首字母应该小写：

```js
function getData() {
}

export default getData
```

- 模块输出一个对象，首字母应该大写

```js
const Person = {
  someCode: {
  }
}

export default Person
```

