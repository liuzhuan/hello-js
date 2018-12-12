# Channel Messaging API

[MDN](https://developer.mozilla.org/en-US/docs/Web/API/Channel_Messaging_API)

Channel Messaging API 允许两个处于浏览器不同 context 脚本直接通信，通过管道直接发送信息。

> 此特性在 Web Workers 中存在

信道（message channel）通过 `MessageChannel()` 构造函数创建，它的两个端口可以通过 `MessageChannel.port1` 和 `MessageChannel.port2` 获取（均为 `MessagePort` 类型）。创建信道的应用使用 `port1`，另一个应用使用 `port2`。

另一个浏览器 context 可以通过 `MessagePort.onmessage` 监听信息，并通过事件的 `data` 属性获取内容。然后通过 `MessagePort.postMessage` 向原文档反馈信息。

如果不想继续传递信息，可以通过 `MessagePort.close` 关闭端口。

## DEMO

[online reading](https://developer.mozilla.org/en-US/docs/Web/API/Channel_Messaging_API/Using_channel_messaging)

```js
var input = document.querySelector('#message-input')
var output = document.querySelector('#message-output')
var button = document.querySelector('button')
var iframe = document.querySelector('iframe')

var channel = new MessageChannel()
var port1 = channel.port1

iframe.addEventListener('load', onLoad)

function onLoad() {
    button.addEventListener('click', onClick)
    port1.onmessage = onMessage
    // Transfer port2 to the iframe
    iframe.contentWindow.postMessage('init', '*', [channel.port2])
}

function onClick(e) {
    e.preventDefault()
    port1.postMessage(input.value)
}

function onMessage(e) {
    output.innerHTML = e.data
    input.value = ''
}

// inside IFrame
var list = document.querySelector('ul')
var port2

window.addEventListener('message', initPort)

function initPort(e) {
    port2 = e.ports[0]
    port2.onmessage = onMessage
}

function onMessage(e) {
    var listItem = document.createElement('li')
    listItem.textContent = e.data
    list.appendChild(listItem)
    port2.postMessage('Message received by IFrame: "' + e.data + '"')
}
```