---
title: vue-cli 自定义配置初始化项目vue+typescript+eslint
tags:
notebook: 前端
---
# vue-cli 自定义配置初始化项目vue+typescript+eslint
上节说到使用vue cli3.0 ，这里就介绍怎么自定义配置吧。记录一下，省得忘了

## 概述
环境：
- win10
- vscode
- npm
- vue cli 4.1.1(3.0以上的都行吧)

## 1. 初始化项目
``` npm
vue create <projectName>
```
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191212152041.png)
然后就要选择是默认还是自定义配置了。
### 1.1 默认配置
vue cli 3.0以上的版本的默认配置，就是包含babel 和 eslint
走默认配置很简单啊，什么都不用管，直接yes，回车，然后就生成了。

最后生成的配置文件(package.json)是这样的。
``` json
{
  "name": "vue-typescript-demo",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build",
    "lint": "vue-cli-service lint"
  },
  "dependencies": {
    "core-js": "^3.4.3",
    "vue": "^2.6.10"
  },
  "devDependencies": {
    "@vue/cli-plugin-babel": "^4.1.0",
    "@vue/cli-plugin-eslint": "^4.1.0",
    "@vue/cli-service": "^4.1.0",
    "babel-eslint": "^10.0.3",
    "eslint": "^5.16.0",
    "eslint-plugin-vue": "^5.0.0",
    "vue-template-compiler": "^2.6.10"
  },
  "eslintConfig": {
    "root": true,
    "env": {
      "node": true
    },
    "extends": [
      "plugin:vue/essential",
      "eslint:recommended"
    ],
    "rules": {},
    "parserOptions": {
      "parser": "babel-eslint"
    }
  },
  "browserslist": [
    "> 1%",
    "last 2 versions"
  ]
}

```

### 1.2 自定义配置
先明确下我的目标：vue + typescript + eslint + pretter
来吧！ （win10 建议使用npm来操作！！！）
#### 1.2.1 选择你需要的模块
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191212155032.png)

#### 1.2.2 选择eslint+prettier
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191212155409.png)

#### 1.2.3
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191212155530.png)

#### 1.2.4
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191212160444.png)

#### 1.2.5 大功告成(:sob:我终于搞出来了)
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191212160444.png)

#### 1.2.6 完整的配置
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191212165027.png)
这里最后有一条：`Save preset as:`是说要把这次的设置新建成一个模版，以后再创建的时候，就可以直接根据这个模版来直接初始化，就不用再一步一步配置了。（就和那个默认模版差不多概念）

最后生成的配置文件是这样的：
``` json
{
  "name": "vue-typescript-eslint",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build",
    "lint": "vue-cli-service lint"
  },
  "dependencies": {
    "core-js": "^3.4.3",
    "vue": "^2.6.10",
    "vue-class-component": "^7.0.2",
    "vue-property-decorator": "^8.3.0",
    "vue-router": "^3.1.3",
    "vuex": "^3.1.2"
  },
  "devDependencies": {
    "@vue/cli-plugin-babel": "^4.1.0",
    "@vue/cli-plugin-eslint": "^4.1.0",
    "@vue/cli-plugin-router": "^4.1.0",
    "@vue/cli-plugin-typescript": "^4.1.0",
    "@vue/cli-plugin-vuex": "^4.1.0",
    "@vue/cli-service": "^4.1.0",
    "@vue/eslint-config-prettier": "^5.0.0",
    "@vue/eslint-config-typescript": "^4.0.0",
    "eslint": "^5.16.0",
    "eslint-plugin-prettier": "^3.1.1",
    "eslint-plugin-vue": "^5.0.0",
    "node-sass": "^4.12.0",
    "prettier": "^1.19.1",
    "sass-loader": "^8.0.0",
    "typescript": "~3.5.3",
    "vue-template-compiler": "^2.6.10"
  }
}

```

:sparkles:tip：
如果选错了，要返回上一步，就`ctrl+c` 退出，重新选择

## 测试的配置
```
Vue CLI v4.2.2
? Please pick a preset: Manually select features
? Check the features needed for your project: Babel, TS, PWA, Router, Vuex, CSS Pre-processors, Linter
? Use class-style component syntax? Yes
? Use Babel alongside TypeScript (required for modern mode, auto-detected polyfills, transpiling JSX)? Yes
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Pick a CSS pre-processor (PostCSS, Autoprefixer and CSS Modules are supported by default): Sass/SCSS (with node-sass)
? Pick a linter / formatter config: Prettier
? Pick additional lint features: Lint on save, Lint and fix on commit
? Where do you prefer placing config for Babel, ESLint, etc.? In package.json
? Save this as a preset for future projects? Yes
? Save preset as: vue-typescript-test-config
```
## 参考资料
- [vue-cli 3.0使用指南(CSDN-往后余生cp)](https://blog.csdn.net/luchuanqi67/article/details/80907107)