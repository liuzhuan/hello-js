# window.localStorage

只读属性 `localStorage` 允许读取同域名下的 `Storage` 对象。同 `sessionStorage` 类似，但更持久。`sessionStorage` 关闭浏览器后就会清空。

存储的数据会被转换为字符串。

切记，`localStorage` 和 `sessionStorage` 存储的数据均对应与页面的协议。

## 语法

```javascript
myStorage = window.localStorage
```

## 用法

```javascript
// set item
localStorage.setItem('myCat', 'Tom')
localStorage.myCat = 'Tom'
localStorage['myCat'] = 'Tom'

// get item
var cat = localStorage.getItem('myCat')

// remove item
localStorage.removeItem('myCat')
```

# window.sessionStorage

几乎与 `localStorage` 相同，故略。

## REF

- [window.localStorage - MDN][mdn]
- [Using the Web Storage API - MDN][api]

[mdn]: https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage
[api]: https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API