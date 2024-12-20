# WHT-UI 组件库

WHT-UI 是一个基于 uni-app 的 UI 组件库，提供了丰富的常用组件，帮助开发者快速构建移动应用。


## 项目演示（H5）

<img src="https://env-00jxh6w9ibri.normal.cloudstatic.cn/plugins/wht-ui.png" alt="WHT-UI项目演示" width="200" style="margin: 10px;">
## 特性

- 🚀 基于 uni-app，支持多端开发
- 📦 提供丰富的基础组件
- 🎨 统一的设计风格
- 📱 移动端优先，适配多种屏幕尺寸
- 🔧 支持按需引入
- 📖 详细的文档和示例

## 平台兼容性

### 框架支持
- ✅ Vue 2

### 平台支持
- ✅ H5
- ✅ 微信小程序
- ✅ App（iOS/Android）


## 安装使用

### 安装

在 uni-app 插件市场中搜索 "WHT-UI" 并安装。

安装完成后，即可直接在页面中使用组件，无需手动引入。

### 组件使用示例

```vue
<template>
  <wht-button type="primary">按钮</wht-button>
</template>
```

## 组件列表

### 基础组件
- Button 按钮
  - 支持类型：primary, success, warning, danger
  - 支持尺寸：large, normal, small, mini
  - 支持状态：loading, disabled

### 表单组件
- Checkbox 复选框
  - 支持单选/多选模式
  - 支持自定义颜色和大小
- DatetimePicker 时间选择器
  - 支持日期、时间、日期时间选择
  - 支持自定义格式化
- Input 输入框
  - 支持多种类型输入
  - 支持清除、密码显示切换
- Radio 单选框
  - 支持自定义颜色和大小
  - 支持禁用状态
- Rate 评分
  - 支持自定义图标和颜色
  - 支持半星评分
- Search 搜索
  - 支持实时搜索和防抖
  - 支持搜索历史
- Select 选择器
  - 支持单选和多选
  - 支持自定义选项内容

### 反馈组件
- Popup 弹出层
  - 支持多个方向弹出
  - 支持自定义内容和动画
- NoticeBar 通知栏
  - 支持滚动播放
  - 支持自定义样式和速度

### 展示组件
- ImgUpload 图片上传
  - 支持多图上传
  - 支持预览和删除
- Picker 选择器
  - 支持单列、多列、联动选择
  - 支持自定义选项内容
- Tabbar 标签栏
  - 支持自定义图标和样式
  - 支持徽标显示
- Tabs 标签页
  - 支持滑动切换
  - 支持自定义样式

### 业务组件
- Lottery 抽奖
  - 支持九宫格抽奖
  - 支持自定义奖品和动画

## 常见问题

### 1. 样式问题
- H5端：建议开启 scoped 样式隔离
- 小程序端：注意避免使用复杂的选择器
- App端：部分样式可能需要平台特定的适配

### 2. 事件处理
- 统一使用 @click 而不是 @tap
- 注意在不同平台上事件触发的时机可能有差异

### 3. 生命周期
- 建议使用 uni-app 统一的生命周期钩子

## 版本记录

### v1.0.0
- 首次发布
- 支持 15+ 基础组件
- 完整的示例和文档

## 赞赏支持

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

## 联系我们

如有问题或建议，欢迎通过以下方式联系我们：
- 提交 [Issues](https://github.com/yourusername/wht-ui/issues)
- 邮箱：your.email@example.com（替换为您的联系邮箱）

## 贡献指南

欢迎提交 Issue 和 Pull Request

## 开源协议

MIT License