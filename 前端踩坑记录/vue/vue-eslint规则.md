# vue-eslint规则
<!-- TOC -->

- [vue-eslint规则](#vue-eslint%e8%a7%84%e5%88%99)
  - [单行校验，让你换行，怎么关闭这个规则](#%e5%8d%95%e8%a1%8c%e6%a0%a1%e9%aa%8c%e8%ae%a9%e4%bd%a0%e6%8d%a2%e8%a1%8c%e6%80%8e%e4%b9%88%e5%85%b3%e9%97%ad%e8%bf%99%e4%b8%aa%e8%a7%84%e5%88%99)
    - [报错信息](#%e6%8a%a5%e9%94%99%e4%bf%a1%e6%81%af)
    - [解决方法](#%e8%a7%a3%e5%86%b3%e6%96%b9%e6%b3%95)
  - [参考资料](#%e5%8f%82%e8%80%83%e8%b5%84%e6%96%99)

<!-- /TOC -->
## 单行校验，让你换行，怎么关闭这个规则
### 报错信息
```
Expected 1 line break before closing tag (`</p>`), but no line breaks found
```
有时候eslint的规则真的非常多余
比如在p标签内加了参数，就非得让你换行
```
<p>{{ msg }}</p>
```
eslint 就报错`Expected 1 line break before closing tag (`</p>`), but no line breaks found`，让你改成这样子
```
<p>
  {{ msg }}
</p>
```
气死，这样其实看上去一点都不直观！
### 解决方法
那就修改规则吧，在eslint规则配置文件里的rules，加上这两句
```node
module.exports = {
  rules: {
    // 单行校验的规则关闭
    'vue/singleline-html-element-content-newline': 'off',
    'vue/multiline-html-element-content-newline': 'off',
  }
}
```

## 参考资料
- [How do I turn off this Eslint error “Expected new line break before and after html tags”?(stackoverflow)](https://stackoverflow.com/questions/54603407/how-do-i-turn-off-this-eslint-error-expected-new-line-break-before-and-after-ht)