## Boolean

所有的数值均可转换为 Boolean 值，其中以下数值转换为 `false`：

```javascript
undefined
null
0
-0
NaN
""
```

除此之外，其他任何数值，均转换为 `true`。空对象和空数组也不例外，比如：

```javascript
var arr = []
if (arr) {
    console.log('Truthy') // => Truthy
} else {
    console.log('Falsy')
}

var obj = {}
if (obj) {
    console.log('Truthy') // => Truthy
} else {
    console.log('Falsy')
}
```

**注意**：虽然空对象和空数组可以转换为 `true`，但它们和 Boolean 直接比较时，却有不同的结果。具体如下：

```javascript
var arr = []
arr == true  // => false
arr == false // => true

var obj = {}
obj == true  // => false
obj == false // => false
```

这是因为 `==` 并不会将类型转换为 Boolean 值。除了空对象和空数组，其他类型亦如此：

```javascript
undefined == false // => false
null == false // => false
```