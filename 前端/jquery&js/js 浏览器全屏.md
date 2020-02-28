# js 浏览器全屏
### 触发全屏
```js
//唤起全屏
  mm.openFullscreen = function (){
    var docElm = document.documentElement;
    //W3C
    if (docElm.requestFullscreen) {
        docElm.requestFullscreen();
    }
    //FireFox
    else if (docElm.mozRequestFullScreen) {
        docElm.mozRequestFullScreen();
    }
    //Chrome等
    else if (docElm.webkitRequestFullScreen) {
        docElm.webkitRequestFullScreen();
    }
  }
```
### 退出全屏
```js
//关闭全屏
  mm.closeFullscreen = function (){
    if (document.exitFullscreen) {
        document.exitFullscreen();
    }
    else if (document.mozCancelFullScreen) {
        document.mozCancelFullScreen();
    }
    else if (document.webkitCancelFullScreen) {
        document.webkitCancelFullScreen();
    }
    else if (document.msExitFullscreen) {
        document.msExitFullscreen();
    }
  }
```
### 监听页面是否全屏，并做出相应处理
```js
 /**
   * 检查是否是全屏状态
   * @return boolean true 就是全屏
   */
  var checkFull = function() {
    var isFull = document.fullscreen || document.mozFullScreen || document.webkitIsFullScreen || document.webkitFullScreen ||document.msFullScreen ;
		if(isFull === undefined) {
      isFull = false;
    } else {
      isFull = true
    }
    return isFull;
  }
  // 在页面大小变化时做处理
  window.onresize = function() {
    if(checkFull()) {
      console.log('全屏')
    } else {
      console.log('退出全屏')
    }
  }
```