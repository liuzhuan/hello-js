# 上传文件

使用 HTML 表单 `<input type="file">` ，可以将用户选择的文件，塞入 POST 请求中。

直到最新，才可以利用 XMLHttpRequest API 将文件上传。XHR2 API，允许你把 File 对象放入到 `send()` 方法中，以便上传文件。

## REF

- 《JavaScript 权威指南》（第六版），18.1.3.4 Uploading a file, p505