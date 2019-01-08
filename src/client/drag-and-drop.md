# HTML 拖放

[online reading](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API)

1. 用户可以拖动 draggable 元素，井将其放到 droppable 元素中。
2. HTML 拖放使用 drag events，它继承自 mouse events。
3. 所有的 drag event 类型都有一个全局的事件处理器。
4. 当从操作系统向浏览器拖放文件时，不会触发 `dragstart` 和 `dragend` 事件。
5. HTML 拖放接口包括 DragEvent, DataTransfer, DataTransferItem 和 DataTransferItemList。
6. DataEvent 接口拥有一个构造函数和一个属性 `dataTransfer`，这是一个 `DataTransfer` 对象。
7. DataTransfer 对象包括拖动事件的状态，比如当前拖放的类型（`copy` 还是 `move`）、拖放的数据（一个或多个元素）、每个拖放元素的类型（MIME 类型）。DataTransfer 对象还有一些方法，可以增删拖放元素。
8. 每个 DataTransfer 对象包含 `items` 属性，它是一个列表，其中每个元素都是 `DataTransferItem` 类型。每个 DataTransferItem 对象表示一个独立的拖放对象。每个元素的 `kind` 属性表示数据的类型（`string` 或 `file`）。每个元素的 `type` 表示它的 MIME 类型。`DataTransferItem` 还提供了获取拖放数据的方法。
9. `DataTransferItemList` 对象是一个 `DataTransferItem` 列表。可以增删清空拖放元素。
10. 为了让一个元素可拖动，需要增加 `draggable` 属性和 `ondragstart` 全局事件监听器。
11. 应用可以自由设定一次拖动中的元素。每个元素都是一种特殊类型的字符串。比如 `text/html`。
12. `dataTransfer` 的 `setData()` 可以增加拖放数据的元素。
13. 可以通过 `setDragImage()` 自定义拖动的图像。
14. `dropEffect` 可以设定拖放操作的视觉反馈，它可以影响拖动时的鼠标样式。可以定义三种 effect: `copy`, `move`, `link`。
15. 浏览器默认会阻止所有元素的拖放效果。除非在元素上指定 `ondragover` 和 `ondrop` 事件侦听函数。
16. 拖放事件中的 `preventDefault()` 可以防止额外的事件处理，比如触摸事件或鼠标事件。
17. 通常使用 `getData()` 获取拖放元素。
18. 对于拖动目标，常用的事件是 `ondragstart` 和 `ondragend`；对于放置区域，最常用的事件是 `ondrop` 和 `ondragover`。

所有的拖放事件

| 事件 | On Event 处理器 | 描述 |
| --- | --- | --- |
| dragstart | ondragstart | 当用户开始拖动元素或文本 |
| dragend | ondragend | 当拖动操作结束时 |
| dragenter | ondragenter | 当拖动的元素进入合法的放置目标 |
| dragexit | ondragexit | 当元素不再是拖放操作的立即选中目标 |
| dragleave | ondragleave | 当拖动的元素离开合法的放置目标 |
| dragover | ondragover | 当一个元素或文本拖放经过一个合法的放置目标 |
| drop | ondrop | 当元素或文本放置到合法的放置目标 |

推荐的拖放类型

[recommended drag types](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API/Recommended_drag_types)

1. `text/plain` 字符串
2. `text/uri-list` URL
3. `text/xml`
4. `text/html`

## 代码片段

标识元素可以拖动

```js
function dragstart_handler(e) {
    console.log('drag start')
    e.dataTransfer.setData('text/plain', e.target.id)
}
```

```html
<p 
    id="p1" 
    draggable="true"
    ondragstart="dragstart_handler(e);">
    This element is draggable.
</p>
```

定义拖放的元素

```js
function dragstart_handler(e) {
    e.dataTransfer.setData('text/plain', e.target.id)
    e.dataTransfer.setData('text/html', '<p>Example Paragraph</p>')
    e.dataTransfer.setData('text/uri-list', 'http://developer.mozilla.org')
}
```

自定义拖放图像

```js
function dragstart_handler(e) {
    var img = new Image()
    img.src = 'example.gif'
    e.dataTransfer.setDragImage(img, 10, 10)
}
```

定义拖放效果

```js
function dragstart_handler(e) {
    e.dataTransfer.dropEffect = 'copy';
}
```

定义放置目标

```html
<div
    id="target"
    ondrop="drop_handler(evnet);"
    ondragover="dragover_handler(event);">
    Drop Zone
</div>
```

```js
function dragover_handler(e) {
    e.preventDefault()
    e.dataTransfer.dropEffect = 'move'
}

function drop_handler(e) {
    e.preventDefault()
    var data = e.dataTransfer.getData('text/plain')
    e.target.appendChild(document.getElementById(data))
}
```

处理放置效果

```html
<p
    id="p1"
    draggable="true"
    ondragstart="dragstart_handler(event);">
    This element is draggable.
</p>
<div
    id="target"
    ondrop="drop_handler(event);"
    ondragover="dragover_handler(event);">
    Drop Zone
</div>
```

```js
function dragstart_handler(e) {
    e.dataTransfer.setData('text/plain', e.target.id)
    e.dataTransfer.dropEffect = 'move'
}

function dragover_handler(e) {
    e.preventDefault()
    e.dataTransfer.dropEffect = 'move'
}

function drop_handler(e) {
    e.preventDefault()
    var data = e.dataTransfer.getData('text/plain')
    e.target.appendChild(document.getElementById(data))
}
```