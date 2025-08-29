## 剔除key相同的项 保留第一个key不一样的项

```tsx
function removeDuplicateByKey(arr, keyName = 'key') {
  return arr.filter((item, index, self) =>
    self.findIndex(i => i[keyName] === item[keyName]) === index
  );
}
```


## 分页函数

```tsx
/**
 * 手动分页函数
 * @param param0 分页选项
 * @param data 数据列表
 */
export function manualPaginate<T extends ObjectLiteral>(
    { page, limit }: IPaginateDto,
    data: T[],
): Pagination<T> {
    let items: T[] = [];
    const totalItems = data.length;
    const totalRst = totalItems / limit;
    const totalPages =
        totalRst > Math.floor(totalRst) ? Math.floor(totalRst) + 1 : Math.floor(totalRst);
    let itemCount = 0;
    if (page <= totalPages) {
        itemCount = page === totalPages ? totalItems - (totalPages - 1) * limit : limit;
        const start = (page - 1) * limit;
        items = data.slice(start, start + itemCount);
    }
    const meta: IPaginationMeta = {
        itemCount,
        totalItems,
        itemsPerPage: limit,
        totalPages,
        currentPage: page,
    };
    return {
        meta,
        items,
    };
}

```


