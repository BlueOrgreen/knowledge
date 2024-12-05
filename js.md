# Javascript 基础知识

## Object.getOwnPropertyDescriptor 

用于获取对象某个属性的描述符的方法，它返回一个对象，其中包含该属性的配置细节
- `value` 属性的值
- `writable` 如果为 `true` 则表示属性值可以被修改
- `enumerable` 如果为 `true` 则表示属性会在 `for……in` 循坏和 `Object.keys()` 中出现
- `configurable` 如果为 `true`，表示属性描述符可以被改变，或者属性可以被删除

```jsx
const obj = { name: "Alice" };
const descriptor = Object.getOwnPropertyDescriptor(obj, "name");

console.log(descriptor);
// 输出: { value: "Alice", writable: true, enumerable: true, configurable: true }
```