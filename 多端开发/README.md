# 多端开发

## 微信小程序

#### rpx

`rpx` 类似于一个带有自动缩放特性的单位，省去了媒体查询的繁琐操作。需要注意的是，它只适用于 `微信小程序`，不是 Web 标准单位

屏幕宽度 / 750 = 1rpx 对应的实际像素值

特点：
- `750rpx` 刚好等于 屏幕宽度（不管设备是多少像素宽）
- 自动适配不同机型、不同分辨率，不需要手动写媒体查询
- 通常配合 `750px` 宽的设计稿 使用



## Taro

CSS样式兼容、不同小程序API的差别

面试介绍： 介绍完成哪些端的应用、以及不同端组件差异的磨平


## ReactNative

能调用原生模块，并且有较好的性能； 通过 `Bridge` 调用一些原生的功能， 比如` 地理位置服务`
