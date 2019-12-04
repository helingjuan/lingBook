---
title: js-调用function(){} 里的属性或者方法
tags: js
notebook: 前端
---
# js-调用function(){} 里的属性或者方法
有时候，把一个函数封装好了，但是有一些地方，又需要调用这个函数中的某个方法，这时候需要用`return` ,把外部可以调用的方法，return出去。

举个例子：
```
function accountListAction(options) {

  //默认配置
  this.options = {
      listTplId: options.listTplId ||  '#account_list_tpl',
      listId: options.listId || 'account_list_content',
      pageId: options.pageId || 'account_page_content',
      listUrl: options.listUrl || path.u('/setting/StadiumConfig/getAccountList2'),
      listUrlParse: options.listUrlParse || {},
      checkItemName: options.checkItemName || 'adm_id'
  };
  /**
   * 列表初始化
   */
  var initPageList = function(parse,idStr) {
    // 一些操作
  }

  /**
   * 选中框内容初始化
   * 这个一定要在表格初始化之后，才能调用，不然会找不到元素
   */
  var initSelectedBox = function(idStr, nameStr) {
    // 一些操作
  }

  /**
   * 获取全部账户,并写入已选中框中
   */
  var getAllData = function() {
    // 一些操作
  }

  /**
   * 获取部分账户,并写入已选中框中,传入的那个id不渲染
   * @param id 不渲染的id
   */
  var getPartData = function(id) {
    // 一些操作
  }

  // 返回，划重点！！！
  return {
    init: function(parse, idStr) {
      initPageList(parse, idStr)
    },
    initSelectedBox: function(idStr, nameStr) {
      initSelectedBox(idStr, nameStr)
    },
    getPartData: function(id) {
      getPartData(id)
    },
    getAllData: function() {
      getAllData()
    }
  }
}
```
看看怎么使用：  
```
/**
 * 账户列表搜索
 */
mm.searchAccountList = function() {
  accountListAction(options).init() //划重点！ 
}
```
