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

## FocusEvent

[blur](https://developer.mozilla.org/en-US/docs/Web/Events/blur)

1. 当元素失去焦点时，抛出 `blur` 事件。它和 `focusout` 区别是，后者可以冒泡。
2. 如果使用 `blur` 作为代理，要么使用 `focusout` 事件，要么将 `addEventListener()` 的 `useCapture` 设为 `true`。
3. [FocusEvent](https://developer.mozilla.org/en-US/docs/Web/API/FocusEvent) 表示焦点相关的事件，包括 `focus`, `blur`, `focusin`, `focusout`。
4. FocusEvent 的继承关系是 `Event <-- UIEvent <-- FocusEvent`。
5. `focus` 和 `focusin` 事件类似，只是后者可以冒泡。

### 代码片段：

```html
<form id="form">
    <input type="text" placeholder="text input">
    <input type="password" placeholder="password">
</form>
```

```js
var form = document.querySelector("#form");

form.addEventListener('focus', function(e) {
    e.target.style.background = 'pink';
}, true);

form.addEventListener('blur', function(e) {
    e.target.style.background = '';
}, true);
```