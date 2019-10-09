---
title: html table中 tr和td 嵌套的易错点 
tags: html
notebook: 前端
---
# html table中 tr和td 嵌套的易错点
这是我遇到过的问题
我的代码大概是这样的
```
// 就是一层tr嵌套一层
<tbody>
<tr>
  <td></td>
  <tr>
  <td></td>
  </tr>
</tr>
</tbody>
```
后来发现，在跨行`rowspan`的时候有问题.
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190929180436.png)

后来仔细看了，发现是**tr与tr是不能直接嵌套的**，如果实在需要嵌套的话，可以在tr里嵌套一个tabel

### 解决
看代码：
```
//css
table {
  text-align: center;
  border-collapse: collapse;
  padding: 0;
  margin: 0;
}
.outTable {
  width: 100%;
  height: auto;
  & td {
    border: 1px solid #ccc;
  }
}
.inTable {
  width: 100%;
  height: 100%;
}
```
```
// html
<div class="center">
    <h4>table的多层嵌套</h4>
    <div class="content">

      <table class="outTable">
        <thead>
          <tr>
            <td width="160px">班级名称</td>
            <td width="150px">学生名称</td>
            <td width="150px">课程类型</td>
            <td width="150px">课程名称</td>
            <td>课程成绩</td>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>信息与计算科学1班</td>
            <td colspan="4">
              <table frame="void" class="inTable">
                <tr>
                  <td width="149px">张三</td>
                  <td colspan="3">
                    <table frame="void" class="inTable">
                      <tr>
                        <td width="149px">理科</td>
                        <td colspan="2">
                            <table frame="void" class="inTable">
                              <tr>
                                <td width="149px">高等数学</td>
                                <td>80</td>
                              </tr>
                              <tr>
                                <td>物理</td>
                                <td>85</td>
                              </tr>
                            </table>
                        </td>
                      </tr>
                      <tr>
                          <td width="149px">文科</td>
                          <td colspan="2">
                              <table frame="void" class="inTable">
                                <tr>
                                  <td width="149px">大学语文</td>
                                  <td>80</td>
                                </tr>
                                <tr>
                                  <td>大学英语</td>
                                  <td>85</td>
                                </tr>
                              </table>
                          </td>
                        </tr>
                    </table>
                  </td>
                </tr>
                <tr>
                  <td width="149px">李四</td>
                  <td colspan="3">
                      <table frame="void" class="inTable">
                        <tr>
                          <td width="149px">理科</td>
                          <td colspan="2">
                              <table frame="void" class="inTable">
                                <tr>
                                  <td width="149px">高等数学</td>
                                  <td>80</td>
                                </tr>
                                <tr>
                                  <td>物理</td>
                                  <td>85</td>
                                </tr>
                              </table>
                          </td>
                        </tr>
                        <tr>
                            <td width="149px">文科</td>
                            <td colspan="2">
                                <table frame="void" class="inTable">
                                  <tr>
                                    <td width="149px">大学语文</td>
                                    <td>80</td>
                                  </tr>
                                  <tr>
                                    <td>大学英语</td>
                                    <td>85</td>
                                  </tr>
                                </table>
                            </td>
                          </tr>
                      </table>
                    </td>
                </tr>
              </table>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
```

这里有几个注意点：
1. table的嵌套只有在td单元格中生效；
2. 由于表格和表格之间的嵌套，导致会出现多个边框，这时候就要在table上加`frame="void"`这个属性；
3. 要在嵌套表格的那个单元格td上根据后续的列数，写好跨列数，比如：`colspan="3"`就是有3列
4. 因为是嵌套table，所以就可以不用考虑跨行的问题了，也就是不用设置`rowspan`了

效果：
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20191009142534.png)