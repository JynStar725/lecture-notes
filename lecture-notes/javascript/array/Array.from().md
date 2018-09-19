## `Array.from()`方法

将一个类似数组的对象（可迭代的，具有Iterator接口--->）转为数组

```js
const foo = document.querySelectorAll('.foo')

const nodes = Array.from(foo)

Object.prototype.toString.call(node) // [object, Array]
```

