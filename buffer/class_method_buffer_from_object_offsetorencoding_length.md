<!-- YAML
added: v8.2.0
-->

* `object` 一个支持 `Symbol.toPrimitive`或`valueOf()`的 object
* `offsetOrEncoding` {number|string} 开始拷贝的索引 或 字符编码, 取决于 `object.valueOf` 或 `object[Symbol.toPrimitive]()`的返回值.
* `length` {number} A length, depending on the value returned either by
  `object.valueOf()` or `object[Symbol.toPrimitive]()`.

对于`valueOf()`函数的返回一个不严格等于`object`的返回值的对象 则执行 `Buffer.from(object.valueOf(), offsetOrEncoding,length)`.
例子:

```js
const buf = Buffer.from(new String('this is a test'));
// <Buffer 74 68 69 73 20 69 73 20 61 20 74 65 73 74>
```
对于支持`Symbol.toPrimitive`的对象, 则执行 `Buffer.from(object[Symbol.toPrimitive(), offsetOrEncoding, length)


For example:

```js
class Foo {
  [Symbol.toPrimitive]() {
    return 'this is a test';
  }
}

const buf = Buffer.from(new Foo(), 'utf8');
// <Buffer 74 68 69 73 20 69 73 20 61 20 74 65 73 74>
```

