# WHT-UI
### 介绍

WHT-UI 是一个轻量级的 uni-app UI 插件，提供常用的UI组件，简单易用。

[uni-app插件市场地址](https://ext.dcloud.net.cn/plugin?id=21321)

### 预览

<div style="display: flex; justify-content: space-around; align-items: center;">
  <div style="text-align: center;">
    <img src="./images/1.png" alt="wht-ui" width="240" style="">
  </div>
  <div style="text-align: center;">
    <img src="./images/2.png" alt="wht-ui" width="240" style="">
  </div>
</div>

### 特性

- 简洁美观的设计风格
- 支持多端运行
- 使用简单，即插即用
- 提供丰富的组件

### 组件列表

#### 基础组件
- Button 按钮：支持多种类型和状态的按钮
- Checkbox 复选框：支持自定义样式的复选框
- Image Upload 图片上传：支持单张/多张图片上传

### 安装教程

1. 在 [uni-app 插件市场](https://ext.dcloud.net.cn/plugin?id=21321) 中搜索 `WHT-UI`
2. 点击 `使用 HBuilderX 导入插件` 或 `下载插件ZIP`
3. 导入到项目后即可使用，无需其他配置

### 使用说明

#### 基础用法

```vue
<template>
  <!-- 按钮组件 -->
  <wht-button type="primary">按钮</wht-button>
  
  <!-- 复选框组件 -->
  <wht-checkbox v-model="checked">复选框</wht-checkbox>
  
  <!-- 图片上传组件 -->
  <wht-img-upload v-model="images" :max="9"></wht-img-upload>
</template>

<script>
export default {
  data() {
    return {
      checked: false,
      images: []
    }
  }
}
</script>
```

### 注意事项

1. 本插件依赖 uni-app 环境，请确保您的项目是 uni-app 项目
2. 组件均以 `wht-` 开头，避免与其他组件库冲突
3. 插件遵循 uni_modules 规范开发，支持 npm 安装或 HBuilderX 导入使用

### 在线文档

[文档地址](https://gitee.com/wht-ui)（完善中）

### 开发计划

- 完善现有组件文档
- 新增更多常用组件
- 优化组件性能
- 提供更多自定义主题选项

### 项目演示（H5）

<img src="https://env-00jxh6w9ibri.normal.cloudstatic.cn/plugins/wht-ui.png" alt="WHT-UI项目演示" width="375" style="margin: 10px;">

### 赞赏支持

如果您觉得这个项目对您有帮助，欢迎赞赏支持，这将鼓励我们持续改进和维护项目。

<div style="display: flex; justify-content: space-around; align-items: center;">
  <div style="text-align: center;">
    <img src="https://env-00jxh6w9ibri.normal.cloudstatic.cn/plugins/wx-qrcode.jpg" alt="微信赞赏码" width="200" style="margin: 10px;">
    <p>微信赞赏</p>
  </div>
  <div style="text-align: center;">
    <img src="https://env-00jxh6w9ibri.normal.cloudstatic.cn/plugins/zfb-qrcode.png" alt="支付宝赞赏码" width="200" style="margin: 10px;">
    <p>支付宝赞赏</p>
  </div>
</div>


感谢您的支持！您的赞赏将用于：
- 持续优化和维护项目
- 开发更多实用功能
- 提供更好的技术支持



### 贡献代码

如果您有好的意见或建议，欢迎给我们提 Issues 或 Pull Requests。

### 开源协议

本项目基于 [MIT](https://opensource.org/licenses/MIT) 协议，请自由地享受和参与开源。