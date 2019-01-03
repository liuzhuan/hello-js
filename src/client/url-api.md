# URL 对象

[online reading](https://developer.mozilla.org/en-US/docs/Web/API/URL/createObjectURL)

1. `URL.createObjectURL()` 可以创建一个 DOMString，代表文件或 Blob 对象的地址。
2. 产生的 URL 生命周期和创建它的文档绑定。
3. 通过 `URL.revokeObjectURL()` 释放 URL。
4. `URL.createObjectURL()` 的参数类型可以是 File, Blob or MediaSource。
5. 每次调用 `createObjectURL()` 都会创建新的 URL 对象，即使作用于同一对象。因此要注意内存管理。