

```tsx
/**
 * 顺序执行一组 setState 函数，然后在状态更新后执行回调
 * @param setStateFns setState 函数组成的数组（同步调用）
 * @param callback 所有状态函数调用之后执行的回调
 */
export const useStateSequence = (
  setStateFns: Array<() => void>,
  callback: () => void,
) => {
  for (const fn of setStateFns) {
    fn() // 同步顺序调用
  }

  // 下一轮事件循环中执行 callback，等待 React 批处理后更新
  setTimeout(callback, 0)
}


  const handleDetail = (r: BusinessCircleDetailType) => {
    useStateSequence(
      [
        () =>
          setBusinessDetailState({
            id: r.id,
            title: r.name,
            type: 'edit',
          }),
      ],
      () => toggleOpenDetail(),
    )
  }
```