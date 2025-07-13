# 🔍什么是 object-fit？
object-fit 是一个 CSS 属性，用于控制可替换元素的内容（如 <img>、<video>）如何适应其容器。它有点类似于 background-size 作用于背景图的方式，但它用于内容本身。

常用于需要控制图像在固定宽高容器中的显示方式。

# ✨ 语法

```
object-fit: fill | contain | cover | none | scale-down;
```

# 🧠 属性值解释

| 值            | 说明                                      |
| ------------ | --------------------------------------- |
| `fill`       | **默认值**，拉伸图像填满容器，可能会**拉伸变形**            |
| `contain`    | 缩放图像以完整显示在容器中，保持比例，**可能有留白**            |
| `cover`      | 缩放图像填满容器，保持比例，**可能裁剪图像**                |
| `none`       | 保持图像原始尺寸，不缩放                            |
| `scale-down` | 根据情况选择 `none` 或 `contain`，即选一个**更小的版本** |


```html
<div class="container">
  <img src="https://via.placeholder.com/300x200" class="fit-img" />
</div>
```

```css
.container {
  width: 200px;
  height: 200px;
  border: 1px solid #ccc;
  overflow: hidden;
}

.fit-img {
  width: 100%;
  height: 100%;
  object-fit: cover; /* 改这里尝试不同值 */
}

```


# ✅ 推荐使用场景

| 场景                  | 推荐值          |
| ------------------- | ------------ |
| 商品/头像展示，要求不留白，裁剪无所谓 | `cover`      |
| 保证完整展示，宁愿留白         | `contain`    |
| 不想缩放或变形，只要原图        | `none`       |
| 简单图片自适应展示           | `scale-down` |


## transform不支持inline

背景: 我在对一个 `span` 标签 添加 `transform` 属性后不生效， 最后通过把元素设置成 `inline-block` 后才生效此CSS

```css
.element {
    transform: 'translateY(1px)';
}
```
