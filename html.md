## border 1px 

border 会占据元素空间，从而可能引起布局变化（比如宽高多了 1px）。而使用 box-shadow 模拟边框，可以避免撑开元素尺寸的问题。

不过要让 box-shadow 看起来像“内边框”并紧贴元素内部边缘，需要用 inset：

#### ✅ 使用 box-shadow 实现内部 1px 边框

```css
box-shadow: inset 0 0 0 1px #d9d9d9;
```
inset：表示内阴影，即在元素内部渲染阴影

0 0 0 1px：水平偏移、垂直偏移、模糊半径、扩展距离

