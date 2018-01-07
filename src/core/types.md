## 类型、数值和变量

JS 类型可分为两个目录：基本类型（`primitive types`）和对象类型（`object types`）。

基本类型包括 number, string, boolean, null, undefined。

### Numbers

JavaScript 里的数字均为 64 位浮点数，其遵循 IEEE 754 标准。最大可至 $$\pm1.7976931348623157 \times 10^{308}$$，最小可达 $$\pm5\times10^{-324}$$。

> 类似 Java, C 或 C++ 中的 `double` 数值类型。

JavaScript 可精确表示整数的范围是 $$-9007199254740992(-2^{53})$$ 至 $$9007199254740992(2^{53})$$。如果使用的整数超过该范围，可能会损失末尾精度。

某些运算（比如数组索引，位运算等）会将数值当作 32 位整数处理。

除数为 0 时，JS 不会报错，而是返回 `Infinity` ，表示无穷大。`0/0` 返回 `NaN`，表示 `Not A Number`，即一个无效数字。在 ES3 中，两者均可读可写，可被代码改变。ES5 做了修正，变为只读。

```javascript
typeof Infinity     // => number
typeof NaN          // => number
```

Number 类定义了一些静态常量，可表示一些数字边界值：

```javascript
Number.POSITIVE_INFINITY // => Infinity
Number.NEGATIVE_INFINITY // => -Infinity
Number.MAX_VALUE         // => 1.7976931348623157e+308
Number.MIN_VALUE         // => 5e-324
Number.NaN               // => NaN
1/Number.POSITIVE_INFINITY // => 0
```