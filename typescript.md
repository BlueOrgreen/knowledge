# Typescript

## ReturnType 

条件类型工具，推断并返回传入函数类型的返回值类型

```ts
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any
```

- `T` 是一个函数类型
- `infer R`  `infer` 关键字用于提取函数返回的类型 `R`

示例
```ts
function getName() {
    return "Join"
}
type NameType = ReturnTye<typeof getName> // string

function getUser() {
    return { id: 1, name: "张三" }
}
type UserType = ReturnTye<typeof getUser>
// { id: number, name: string }
```

用处: 可以复用函数的返回值类型, 不需要重新去声明