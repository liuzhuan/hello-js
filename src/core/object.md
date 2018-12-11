# Object 属性和方法

## freeze()

[mdn](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)

`Object.freeze()` 可以冻结对象。被冻结对象不可更改，无法新增、删除属性，无法改变属性的枚举性、配置性和可读写特性。另外，冻结对象的原型链也无法更改。`freeze()` 的返回值是传入的参数。

```js
const object1 = {
    property1: 42
}

const object2 = Object.freeze(object1)

object2.property1 = 33
// Throws an error in strict mode

console.log(object2.property1)
// => 42

object1 === object2
// => true
```

真实世界的[例子](https://github.com/vuejs/vue/blob/628c1b7f5b298e13975d880c73e8fc2893628c2e/src/shared/util.js#L3)：

```js
// vuejs/vue/src/shared/util.js
export const emptyObject = Object.freeze({})
```

## create()

[mdn](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create)

`Object.create()` 使用现有对象当作原型链，创建新对象。

```js
// Object.create(proto[, propertiesObject])
const person = {
    isHuman: false,
    printIntorduction: function() {
        console.log(`My name is ${this.name}. Am I human? ${this.isHuman}`)
    }
}

const me = Object.create(person)

me.name = "Matthew"
me.isHuman = true

me.printIntroduction()
```

现实世界的[例子](https://github.com/vuejs/vue/blob/d780dd2e2adcf71f40c086055a659a9a2b4a8282/src/shared/util.js#L102)：

```js
// vuejs/vue/src/shared/util.js
export function makeMap(str, expectsLowerCase) {
    const map = Object.create(null)
    const list = str.split(',')
    for (let i = 0; i < list.length; i++) {
        map[list[i]] = true
    }
    
    return expectsLowerCase
    	? val => map[val.toLowerCase()]
    	: val => map[val]
}
```

