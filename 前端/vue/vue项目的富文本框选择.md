# vue项目的富文本框选择

## 曾经用过的

- 百度的ueditor （已经不维护了）
- ckeditor (目前传统项目中用的这个)

## 网上推荐的

- wangEditor
- vue-quill-editor 图片默认转base64
- tinymce (最后选了它的vue版本[tinymce-vue](https://github.com/tinymce/tinymce-vue))老牌的富文本公司，不管是文档还是配置的自由度都很好
据说基于vue的没有什么较好的富文本框

### 选tinymce的几个理由

1. 免费
2. 可以按需求，自定义富文本框
3. 文档全面
4. 使用的人很多
5. 可以直接复制word里的文本和格式过去（最重要一点）
6. 功能强大

> 楼主列举了很多富文本但并没有列举任何 vue 相关的富文本，主要是因为富文本真的比想象中复杂，在前面的文章里也说过了，其实用 vue 封装组件很方便的，没必要去用人家封装的东西。什么 vue-quill vue-editor 这种都只是简单包了一层，没什么难度的。还不如自己来封装，灵活性可控性更强一点。还有一点基于 vue 真没什么好的富文本，不像 react 有 facebook 出的 draft-js，ory 出的 editor，这种大厂出的产品。
> ——来源资料1
> 
## 参考资料
- [富文本(vue-element-admin)](https://panjiachen.github.io/vue-element-admin-site/zh/feature/component/rich-editor.html#%E5%B8%B8%E8%A7%81%E5%AF%8C%E6%96%87%E6%9C%AC)
- [tinymce-vue](https://github.com/tinymce/tinymce-vue)
- [tiny的demo](https://www.tiny.cloud/docs/demo/full-featured/)