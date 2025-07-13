## ReturnType

ReturnType<T> 是 TypeScript 中的一个 内置泛型工具类型（Utility Type），用于 提取函数类型的返回值类型。它非常适合在复杂项目中，复用函数返回值类型，保持类型一致性。

✅ 一、语法

```ts
ReturnType<T>  T 是一个函数类型。
```

ReturnType<T> 会提取该函数的返回值类型。

🧠 二、为什么使用 ReturnType？

避免重复写类型。

保持类型自动同步，防止返回类型修改后忘了更新使用的地方。

🛠️ 三、基本使用示例

示例 1：提取函数的返回类型

```ts

function getUser() {
  return {
    id: 1,
    name: 'Alice',
  };
}

// 用 ReturnType 提取返回类型
type User = ReturnType<typeof getUser>;

const user: User = {
  id: 1,
  name: 'Alice',
};
```

✅ 说明：typeof getUser 是函数类型，ReturnType<typeof getUser> 就是 { id: number; name: string }。

示例 2：配合泛型函数使用

```ts

function wrap<T>(value: T) {
  return {
    data: value,
    success: true,
  };
}

type WrappedString = ReturnType<typeof wrap<string>>;

// 等价于：
/*
type WrappedString = {
  data: string;
  success: boolean;
}
*/

const result: WrappedString = {
  data: 'hello',
  success: true,
};
```

🧪 四、自定义实现 ReturnType（了解原理）
虽然 TS 内置了 ReturnType，但我们也可以尝试用 infer 自定义实现：

```ts
type MyReturnType<T> = T extends (...args: any[]) => infer R ? R : never;
```

解读：
- T extends (...args: any[]) => infer R：表示 T 是一个函数类型。

- infer R：TypeScript 会“推断”函数的返回类型 R。

- 如果 T 是函数类型，就返回 R；否则返回 never。

使用：

```ts
function add(a: number, b: number): number {
  return a + b;
}

type AddReturn = MyReturnType<typeof add>; // number
```

📚 五、适用场景总结

| 场景          | 说明                      |
| ----------- | ----------------------- |
| 接口数据统一类型    | 避免硬编码数据结构               |
| 多处用到函数返回值类型 | 保证返回类型同步更新              |
| 封装工具函数      | 与 `Parameters<T>` 等搭配使用 |



✅ 总结
ReturnType<T> 提取函数 T 的返回类型。

可以配合 typeof 一起使用。

支持复杂的泛型函数提取。

可自定义实现：T extends (...args: any[]) => infer R ? R : never。


## NonNullable


```ts
const operationColumn = [ ... ] as NonNullable<TableProps['columns']>;
```

这里的 `NonNullable<TableProps['columns']>` 的意思是：

✅ 确保 `columns` 不是 `null` 或 `undefined`

TypeScript 中的 `NonNullable<T>` 是一个内置工具类型，它会从类型 `T` 中移除 `null` 和 `undefined`：


```ts
type NonNullable<T> = T extends null | undefined ? never : T;
```

🧠 举个例子说明：假设 `TableProps['columns']` 的类型是：

```ts
type columns = ColumnType[] | null | undefined;
```


那 `NonNullable<TableProps['columns']>` 就是 `ColumnType[]` 去除了 `null` 和 `undefined`


