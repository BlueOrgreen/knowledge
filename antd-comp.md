
## getValueFromEvent

`getValueFromEvent` 是 Ant Design 表单组件 <Form.Item /> 的一个属性，它用于 自定义从组件触发的事件中提取值的方式。

> 一句话总结：当你用了一些自定义组件或特殊组件（比如 `DatePicker`、`Upload` 等），它们的 `onChange` 返回的值不是你想要的表单值结构时，可以用 `getValueFromEvent` 把事件值转换成你想要的。


#### 💡 常见使用场景

```tsx
<Form.Item name="username">
  <Input />
</Form.Item>
```

此时 `<Input />` 触发 `onChange(e)`，表单会自动取 `e.target.value`

但有些组件（比如 `DatePicker`）并不会传 `e.target.value`，而是直接传值（比如 moment 对象）。


#### ✅ 结合 <DatePicker /> 示例

<bold>🌟 目标：我们希望在表单中选日期时，获取的值是字符串格式（如 YYYY-MM-DD），而不是 moment 对象。</bold>

```tsx
import React from 'react';
import { Form, DatePicker, Button } from 'antd';
import dayjs from 'dayjs';

const MyForm = () => {
  const [form] = Form.useForm();

  const onFinish = (values) => {
    console.log('提交的表单值：', values);
  };

  return (
    
    <Form form={form} onFinish={onFinish}>
     <Form.Item
          getValueFromEvent={(value: any) => {
            return value ? value.format('YYYY-MM-DD') : undefined
          }}
          getValueProps={(value: any) => ({
            value: value ? dayjs(value) : [],
          })}
          label="开业日期"
          name={resolveName(injectedKey, 'openDate')}
          rules={[{ required: true, message: '请选择开业日期' }]}
          {...formItemStyle}
        >
          <DatePicker picker="month" style={{ width: '100%' }} />
        </Form.Item>
    </Form>
  );
};

export default MyForm;
```

# getPopupContainer

在 Ant Design 里，很多组件（比如：Select、Cascader、Dropdown、DatePicker 等）都会在「body」里「挂载一个悬浮层」用来展示下拉框、弹出菜单。

默认行为是：
这个浮层（popup、dropdown）会插到 `document.body` 里。

## ✅ 📌 为什么要用 getPopupContainer？

`getPopupContainer` 是用来 `「指定这个下拉框的挂载节点」`的。

> 让它不再默认挂到 `body`，而是挂到你指定的元素上。

## ✅ 📌 典型用法

⭐ 挂到触发节点的父节点

```tsx
<Select
  getPopupContainer={(triggerNode) => triggerNode.parentNode}
/>
```

⭐ 挂到指定的容器

```tsx
<Select
  getPopupContainer={() => document.getElementById('my-container')}
/>
```

⭐ 挂到全局 body（默认行为）

```tsx
<Select
  getPopupContainer={() => document.body}
/>
```


