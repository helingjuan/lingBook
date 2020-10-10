# vue-ts 封装svgIcon
<!-- TOC -->

- [vue-ts 封装svgIcon](#vue-ts-%e5%b0%81%e8%a3%85svgicon)
  - [概述](#%e6%a6%82%e8%bf%b0)
  - [需要的依赖](#%e9%9c%80%e8%a6%81%e7%9a%84%e4%be%9d%e8%b5%96)
  - [开搞](#%e5%bc%80%e6%90%9e)
    - [1.在components下封装svgIcon组件](#1%e5%9c%a8components%e4%b8%8b%e5%b0%81%e8%a3%85svgicon%e7%bb%84%e4%bb%b6)
    - [2.在src下新建svgIcons文件夹](#2%e5%9c%a8src%e4%b8%8b%e6%96%b0%e5%bb%basvgicons%e6%96%87%e4%bb%b6%e5%a4%b9)
    - [3. 在vue.config.ts里进行svg的loader配置](#3-%e5%9c%a8vueconfigts%e9%87%8c%e8%bf%9b%e8%a1%8csvg%e7%9a%84loader%e9%85%8d%e7%bd%ae)
    - [4. 在main.ts里引用](#4-%e5%9c%a8maints%e9%87%8c%e5%bc%95%e7%94%a8)
    - [5. 使用](#5-%e4%bd%bf%e7%94%a8)
  - [目前存在的一个问题](#%e7%9b%ae%e5%89%8d%e5%ad%98%e5%9c%a8%e7%9a%84%e4%b8%80%e4%b8%aa%e9%97%ae%e9%a2%98)
  - [参考资料](#%e5%8f%82%e8%80%83%e8%b5%84%e6%96%99)

<!-- /TOC -->
## 概述

因为一些场景需要图标，就用svg图标了
那么就来封装吧
以下都是参考最后的参考资料完成的！ 感谢他们！！！

## 需要的依赖

- `svg-sprite-loader`

安装依赖

```node
npm i svg-sprite-loader -D
```

## 开搞

### 1.在components下封装svgIcon组件

```
<template>
  <svg :class="svgClass" aria-hidden="true" v-on="$listeners">
    <use :xlink:href="iconName" />
  </svg>
</template>

<script lang="ts">
import  { Vue, Component, Prop } from 'vue-property-decorator'

@Component
export default class SvgIcon extends Vue{
  @Prop({
    type: String,
    required: true,
    default: ''
  })
  private iconClass!: string
  @Prop({
    type: String,
    required: false,
    default: ''
  })
  private className!: string

  private get iconName() {
    return `#icon-${this.iconClass}`
  }
  private get svgClass() {
    if (this.className) {
      return `svg-icon ` + this.className
    } else {
      return `svg-icon`
    }
  }
}
</script>

<style lang="scss" scoped>
.svg-icon {
  width: 1em;
  height: 1em;
  vertical-align: -0.15em;
  fill: currentColor;
  overflow: hidden;
}
</style>
```

### 2.在src下新建svgIcons文件夹
然后在svgIcons文件夹里建svg文件夹，用来专门存放svg图标文件
再在svgIcons文件夹下，新建一个`index.ts`,用来引入svgIcon组件，并全局注册

```typescript
// 引入 svgIcons 组件并全局注册
// 实现自动引入 @/src/svgIcons 下面所有的图标
// require.context("./svg", false, /.svg$/); 这行代码就会去 svg文件夹（不包含子目录）下面的找所有文件名以 .svg结尾的文件能被 require 的文件。
// 更直白的说就是 我们可以通过正则匹配引入相应的文件模块
// require.context 的三个参数：
//   directory：说明需要检索的目录
//   useSubdirectories：是否检索子目录
//   regExp: 匹配文件的正则表达式
import Vue from 'vue'
import SvgIcon from '@/components/SvgIcon'// svg组件
// import SvgIcon from '../../components/SvgIcon.vue'// svg组件

// register globally
Vue.component('svg-icon', SvgIcon)
const req = require.context('./svg', false, /\.svg$/)
const requireAll = (requireContext: any) => requireContext.keys().map(requireContext)
requireAll(req)
```

### 3. 在vue.config.ts里进行svg的loader配置
这里要注意一下！实在`chainWebpack`这个配置项里配置的！(我在这里卡了很久:sob:)

```node
module.exports = {
 chainWebpack: config => {
    // 基础的loader
    const svgRule = config.module.rule('svg')
    // svg相关配置
    svgRule.uses.clear()
    svgRule
      .use('svg-sprite-loader')
      .loader('svg-sprite-loader')
      .options({
        symbolId: 'icon-[name]'
      })
  },
  configureWebpack: config => {
    // 一些其他配置
  }
}
```
### 4. 在main.ts里引用
```node
// 引入svg图标
import './svgIcons'
```
大概这样就完工了
那怎么用呢，很简单
### 5. 使用
这里注意一下，因为上面我们已经全局注册了，所以这里就不需要再引入组件什么的了。可以直接用！
```
<svg-icon icon-class="024"/>
```
024就是指`024.svg`这个图标文件
## 目前存在的一个问题
ts会在`svgIcons/index.ts`里报错说，`Cannot find module '@/components/SvgIcon'`
emmmm  但是其实图标文件已经可以显示出来
这个问题，暂时不知道为什么
我哭:cry:
没办法，就先暂时放着吧
## 参考资料
- [基于Typescript的Vue项目中使用svg图标(喵巨人笔记)](http://www.wmm66.com/index/article/detail/id/108.html)
