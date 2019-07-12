---
title: Element-ui的DatePicker使用
tags: element-ui
notebook: 前端
---
# Element-ui的DatePicker使用
![](https://raw.githubusercontent.com/heihuahe/myGallery/master/noteImage/20190712111711.png)
### 获取DatePicker的值（有格式的）
DatePicker有提供个change事件，当input的值改变时触发，返回值和文本框一致。
```
<el-date-picker
            v-model="logEnd"
            type="date"
            placeholder="日期"     @change="timeChange">
        </el-date-picker>
timeChange(val) {
  console.log(val)// val 就是文本框的值
}
```
### 设置特定的日期范围
```
<el-date-picker
       v-model="value"
       type="date"
       placeholder="选择日期"
       :picker-options="pickerOptions">
</el-date-picker>
data() {
  value: '',
  pickerOptions: this.dateSelect()
}
```
#### 情景1：选择今天以及今天之后的日期
```
methods: {
  dateSelect() {
    return {
      disabledDate(time) {
        return time.getTime() < Date.now() -8.64e7;
      }
    } 
  }
}
```
#### 情景2：选择今天及今天之前的日期
```
methods: {
  dateSelect() {
    return {
      disabledDate(time) {
        return time.getTime() > Date.now() -8.64e6;
      }
    } 
  }
}
```
#### 情景3：选择今天之前的日期，不包含今天
```
methods: {
  dateSelect() {
    return {
      disabledDate(time) {
        return time.getTime() > Date.now();
      }
    } 
  }
}
```
#### 情景4：选择今天之后的日期，不包含今天
```
methods: {
  dateSelect() {
    return {
      disabledDate(time) {
        return time.getTime() < Date.now();
      }
    } 
  }
}
```
#### 情景5：选择3个月之前到今天的日期
```
methods: {
  dateSelect() {
    return {
      disabledDate(time) {
        let curDate = (new Date()).getTime();
        let three = 90 * 24 * 3600 * 1000;
        let threeMonths = curDate - three;
        return time.getTime() > Date.now() || time.getTime() < threeMonths;;
      }
    } 
  }
}
```

### 两个DatePicker 组合使用
情况1： 开始日期和结束日期都只能选择**早于当天**的日期；
开始日期范围：今天之前的日期；
结束日期范围：开始日期到今天；
若先选结束日期，再选开始日期，则开始日期范围为：到结束日期之前
```
<template>
  <div class="block">
    <span class="demonstration">默认</span>
    <el-date-picker
      v-model="value2"
      align="right"
      type="date"
      placeholder="选择日期"
      :picker-options="startDatePicker">
    </el-date-picker>
    <el-date-picker
      v-model="value3"
      align="right"
      type="date"
      placeholder="选择日期"
      :picker-options="endDatePicker">
    </el-date-picker>
  </div>
</template>
```
```
data() {
      return {
          value2: '',
          value3: '',
          startDatePicker:this.beginDate(),
        endDatePicker:this.processDate()
      };
    },
    methods: {
      beginDate(){
        let self = this
        return {
          disabledDate(time){
          return time.getTime() > Date.now()//开始时间不选时，结束时间最大值小于等于当天
             }
           }
      },
      //提出结束时间必须大于提出开始时间
      processDate(){
        let self = this
        return {
          disabledDate(time){
            if(self.value2){
              return new Date(self.value2).getTime() > time.getTime() || time.getTime() > Date.now()
            }else{
              return time.getTime() > Date.now()//开始时间不选时，结束时间最大值小于等于当天
            }
          }
        }
      }
    }
```

### 参考资料
- [Element 官方文档](https://element.eleme.cn/#/zh-CN/component/date-picker)
- [关于element-ui日期选择器disabledDate使用心得(博客园——tt-wedos)](https://www.cnblogs.com/hrlin/p/8778630.html)
- [【ElementUI】日期选择器时间选择范围限制(博客园——ipCoder)](https://www.cnblogs.com/xjcjcsy/p/7977966.html)
