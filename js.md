

const data = [
  {
    categoryNo: 'project-info',
    categoryName: '项目概况',
    subCategoryType: 1,
    fieldList: [
      {
        fieldNo: 'name',
        fieldName: '项目名称',
        type: 'input',
      },
      {
        fieldNo: 'projectCode',
        fieldName: '项目编码',
        type: 'input',
      },
      {
        fieldNo: 'area',
        fieldName: '面积',
        type: 'number',
      },
      {
        fieldNo: 'contractedArea',
        fieldName: '签约面积',
        type: 'number',
      },
      {
        fieldNo: 'handoverDate',
        fieldName: '交铺日期',
        type: 'date-picker',
      },
      {
        fieldNo: 'approveDate',
        fieldName: '审批通过日期',
        type: 'custom',
        linkUrl: 'XXXX',
        linkinput: '查看审批记录',
      },
    ],
  },
  {
    categoryNo: 'store-construction-info',
    categoryName: '门店施工信息',
    subCategoryType: 2,
    subCategoryList: [
      {
        categoryName: '1.施工方',
        categoryNo: 'contractor',
        fieldList: [
          {
            fieldNo: 'contractor',
            fieldName: '施工方',
            type: 'input',
          },
          {
            fieldNo: 'projectManager',
            fieldName: '项目经理（施工方）',
            type: 'input',
          },
          {
            fieldNo: 'supervisor',
            fieldName: '工程监理（壹荟）',
            type: 'input',
          },
          {
            fieldNo: 'leaseContract',
            fieldName: '店铺最终租赁CAD文件',
            type: 'file',
          },
          {
            fieldNo: 'spacePhotosIn',
            fieldName: '图片',
            type: 'image',
          },
        ],
      },
      {
        categoryName: '2.智能安装设备',
        categoryNo: 'intelDevicesCategory',
        fieldList: [
          {
            fieldNo: 'intelDevices',
            type: 'table',
            fieldName: '',
            tableFields: [
              {
                fieldNo: 'tableFiledKey-1',
                fieldName: '表格栏一',
                type: 'input',
              },
              {
                fieldNo: 'tableFiledKey-2',
                fieldName: '表格栏二',
                type: 'input',
              },
              {
                fieldNo: 'tableFiledKey-3',
                fieldName: '表格栏三',
                type: 'custom',
              },
            ],
          },
          {
            fieldNo: 'intelDevices22',
            type: 'input',
            fieldName: '制造设备',
          },
        ],
      },
    ],
  },
]


```js
function findFieldType(data, targetKey) {
  data.forEach((item) => {ar
    const { fieldList } = item
    fieldList?.forEach((it) => {
      if (it.fieldNo === targetKey) {
        return it.type
      }
    })
  })
  return undefined
}
```

⚠️ 在 forEach 里的 return 只会结束当前的回调函数，不会中断外层的 forEach，也不会让外层函数提前返回。

换句话说：

✅ 这里的 return it.type 是 只 return 给了内层的 forEach 回调函数
❌ 它不会把 it.type return 给 findFieldType 函数

结果是你的整个外层函数依然会跑完整个两层循环，最后返回的是 undefined。


✅ 如果你想“找到就返回”要怎么改？
你要用能「中断」遍历的循环结构，比如：

① 用 for...of（推荐）

```js
function findFieldType(data, targetKey) {
  for (const item of data) {
    const { fieldList } = item
    if (fieldList) {
      for (const it of fieldList) {
        if (it.fieldNo === targetKey) {
          return it.type
        }
      }
    }
  }
  return undefined
}
```


② 用普通的 for 循环（也可以）

```js
function findFieldType(data, targetKey) {
  for (let i = 0; i < data.length; i++) {
    const fieldList = data[i].fieldList
    if (fieldList) {
      for (let j = 0; j < fieldList.length; j++) {
        if (fieldList[j].fieldNo === targetKey) {
          return fieldList[j].type
        }
      }
    }
  }
  return undefined
}
```


③ 用 flatMap / find（ES6/函数式）
如果你喜欢「链式」写法，可以把所有 fieldList 摊平再找：

```js
function findFieldType(data, targetKey) {
  return data
    .flatMap(item => item.fieldList ?? [])
    .find(it => it.fieldNo === targetKey)
    ?.type
}

```