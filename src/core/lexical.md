## 词汇结构

词汇结构（Lexical Structure）表示某一语言的基本语法规则，比如变量名是什么样，注释分隔符是什么，语句之间如何分隔？

### 字符集

ES3 规范要求支持 Unicode v2.1+ 字符集，ES5 支持 Unicode v3+ 字符集。

JS 中的空白符号包括：普通空格（`\u0020`），制表符（`\u0009`），垂直制表符（`\u000B`），换页符（`\u000C`），非换行空格（`\u00A0`），字节顺序标记（`\uFEFF`），以及 Unicode Z 目录下的所有字符。

JS 将这些字符当作行结束符：换行符（`\u000A`），回车（`\u000D`），行分隔符（`\u2028`），段分隔符（`\u2029`）。

对于尚未支持 Unicode 的设备，可使用 Unicode 转换码表示 Unicode 字符。即用 6 个 ASCII 字符表示任意一个 16 位 Unicode 码点（codepoint）：`\u` 开头，后跟 4 个 16 进制数字。比如 `é` 的 Unicode 转换码是 `\u00E9`，因而如下两字符相等：

```javascript
"café" === "caf\u00E9" // => true
```

### 标识符和关键字

严格模式下，禁止使用 `arguments`, `eval` 作为变量名，函数名或参数名。🈲️

JS 还预定义了一些全局变量和函数，使用时记得避开这些名称：

```
encodeURI   Infinity    Number  RegExp
...
URIError    NaN         JSON    Math
```

### 可选的逗号

逗号非必需，但有时逗号的缺失会造成歧义。