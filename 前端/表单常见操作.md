---
title: select
tags: 
notebook: 
---
# 表单常见操作
### select 
#### 获取select里的值
获取select 选中的 text :
    $("#ddlregtype").find("option:selected").text();

获取select选中的 value:
    $("#ddlregtype ").val();

获取select选中的索引:
    $("#ddlregtype ").get(0).selectedindex;
设置select:
设置select 选中的索引：
    $("#ddlregtype ").get(0).selectedindex=index;//index为索引值

设置select 选中的value：
    $("#ddlregtype ").attr("value","normal“);
    $("#ddlregtype ").val("normal");
    $("#ddlregtype ").get(0).value = value;

设置select 选中的text:

    var count=$("#ddlregtype option").length;
      for(var i=0;i<count;i++)
         {           if($("#ddlregtype ").get(0).options[i].text == text)
            {
                $("#ddlregtype ").get(0).options[i].selected = true;
                break;
            }
        }
    $("#select_id option[text='jquery']").attr("selected", true);

设置select option项:

    $("#select_id").append("<option value='value'>text</option>");  //添加一项option
    $("#select_id").prepend("<option value='0'>请选择</option>"); //在前面插入一项option
    $("#select_id option:last").remove(); //删除索引值最大的option
    $("#select_id option[index='0']").remove();//删除索引值为0的option
    $("#select_id option[value='3']").remove(); //删除值为3的option
    $("#select_id option[text='4']").remove(); //删除text值为4的option

清空 select:

    $("#ddlregtype ").empty();