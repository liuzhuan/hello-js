# 上传文件

使用 HTML 表单 `<input type="file">` ，可以将用户选择的文件，塞入 POST 请求中。

直到最新，才可以利用 XMLHttpRequest API 将文件上传。XHR2 API，允许你把 File 对象放入到 `send()` 方法中，以便上传文件。

1. 通过监听 `change` 事件可以获取选择的文件列表，该列表存储在 `e.target.files` 中。
2. 列表的每个元素都是 `File` 类型。每个 `File` 包含 `name`, `size`, `type` 等主要属性。

File 元素包含的主要属性

1. `name` 文件名称
2. `size` 文件大小，以字节为单位
3. `type` 图片类型，比如 `"image/jpeg"`
4. `lastModified` 上次修改时间戳，以毫秒为单位

## REF

- 《JavaScript 权威指南》（第六版），18.1.3.4 Uploading a file, p505