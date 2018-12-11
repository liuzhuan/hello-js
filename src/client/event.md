# DOM 事件

## Passive Event Listeners

[online reading](https://zhuanlan.zhihu.com/p/24385322)

`passive` 事件监听器，是一种新的 DOM 规范，可以提高页面的滑动流畅度。通过将监听器标记 `{ passive: true }`，表明在其中不会调用 `preventDefault` 函数。

```js
function handler() {
    console.log('DDFE')
}

document.addEventListener('mousewheel', handler, { passive: true })
```

以前的第三个参数是 `true|false`。

兼容性，从 Chrome 51 或 Firefox 49 开始。

## 判断是否支持

```js
var supportsPassive = false

document.createElement('div').addEventListener('test', function(){}, {
    get passive() {
        supportsPassive = true
        return false
    }
})
```

真实世界的[例子](https://github.com/vuejs/vue/blob/d780dd2e2adcf71f40c086055a659a9a2b4a8282/src/core/util/env.js#L21-L33)：

```js
// vuejs/vue/core/util/env.js
let supportsPassive = false
if (inBrowser) {
    try {
        const opts = {}
        Object.defineProperty(opts, 'passive', {
            get() {
                supportsPassive = true
            }
        })
        window.addEventListener('test-passive', null, opts)
    } catch (e) {}
}
```