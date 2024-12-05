# CSS 知识

## transform不支持inline

背景: 我在对一个 `span` 标签 添加 `transform` 属性后不生效， 最后通过把元素设置成 `inline-block` 后才生效此CSS

```css
.element {
    transform: 'translateY(1px)';
}
```