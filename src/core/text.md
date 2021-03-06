## 文本

JS 的文本使用 string 类型，它表示 16-bit 字符的序列。string 的长度代表 16-bit 字符的数量。

JS 使用 UTF-16 编码字符集，string 为一系列无符号 16-bit 数值。最常用的 Unicode 字符（来自 `Basic Multilingual Plane` **基本多语种平面**的字符）的码点用一个 16-bit 表示足矣。有的 Unicode 字符码点超过 16-bit，按照 UTF-16 编码规则，需用两个 16-bit 字符表示，称之为**代理对**(`surrogate pair`)。

这就意味着，长度为 2 的 string，有时候表示的是一个 Unicode 字符。比如：

```javascript
var p = 'π' // π 是一个字符，码点为 0x03c0
var e = '𝑒' // 𝑒 是两个字符，码点是 0x1d452
p.length    // => 1
e.length    // => 2, UTF-16 编码是两个 16-bit 数值："\ud835\udc52"
```

### JS 的转义字符

转义字符 `/` 能赋予普通字符新的含义。除了常见的 `\n`, `\t` 外，`\x XX` 表示两个 16 进制字符 `XX` 代表的 Latin-1 字符。`\u XXXX` 表示 4 个 16 进制字符 `XXXX` 代表的 Unicode 字符。

```javascript
'\xA9'      // => ©
'\u03c0'    // => π
```

### 处理字符串

JS 内置了很多字符串处理函数，比如：

```javascript
var s = 'hello, world'
s.charAt(0)
s.charCodeAt(0)
s.substring(1, 4) // 起始位置到结束位置
s.slice(1, 4)     // 起始位置到结束位置，位置可以是负数
s.indexOf('l')    // => 2
s.indexOf('l', 3) // => 3
```

### 正则表达式

JS 可以使用 `RegExp()` 构造函数，也可以使用字面量 `/regexp/` 创建正则表达式。

RegExp 和 string 定义了很多模式匹配的方法：

```javascript
var text = 'testing: 1, 2, 3'
var pattern = /\d+/g
pattern.exec(text)  // => ['1', index:9, input: 'testing: 1, 2, 3']
pattern.test(text)      // => true
text.search(pattern)    // => 9, 第一个匹配位置
text.match(pattern)     // => ['1', '2', '3']
text.replace(pattern, '#')  // => 'testing: #, #, #'
text.split(/\D+/)   // => ['', '1', '2', '3']
```