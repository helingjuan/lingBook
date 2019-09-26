---
title: ajax return 的坑 
tags: 坑
notebook: 前端
---
# ajax return 的坑
场景是这样的，有一个地方需要调用3-5个接口，且每个接口都需要根据在上一个接口的返回数据进行处理，层层嵌套了。然后，最后这个大函数，又需要返回一个状态true or false，然后我就直接在ajax的success方法里，各种return了。   

这时候，跑到最后，发现这个大函数，return的是一个undefined。这就说明我的return有问题。emmmmm 难受了

#### 解决
这里需要明确的是，ajax中的success方法，其实也只是一个函数，return只是结束这个函数而已。
遇到这种嵌套的请求的时候，要把ajax的请求都改成同步的`async: false`

```
mm.apiAjax({
                url: path.u('/training/sign/addStudent'),
                data: d,
                async: false, //要把请求改成同步的！！！敲重点！！
                success: function(res) {
                  if(!res.is_error) {
                    layer.msg('学员信息关联成功！', {time: 1500})
                    isSuccess = true
                  } else {
                    layer.msg(res.msg, {time: 1500})
                    isSuccess = false
                  }
                }
              })
```

