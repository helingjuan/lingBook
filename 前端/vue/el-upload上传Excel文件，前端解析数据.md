---
title: el-upload上传Excel文件，前端处理数据
tags:
notebook: 前端
---
# el-upload上传Excel文件，前端解析数据
上传有2种方式，数据由前端解析还是后端解析，传统的都是直接把excel文件通过二进制传给后端，然后后端自行解析excel文件里的数据。

这里，我们用的是，前端解析数据的方式，就是**前端直接解析Excel里的数据，然后给后端传的就是Excel文件里的数据**


## 概述
前提条件：使用了插件xlsx

模版
注意！！这个`:auto-upload="false"`一定要写，不然会重复请求接口2次的。
这里上传文件是通过on-change里绑定的方法importExcel方法的
```
<div v-show="active === 1" class="pt-20 alignCenter">
  <el-upload
    class="upload-demo" drag action="" :on-preview="handlePreview" :on-change="importExcel"
    :on-remove="handleRemove" :on-success="uploadSuccess" name="file" :auto-upload="false"
  >
    <i class="el-icon-upload" />
    <div class="el-upload__text">
      将文件拖到此处，或<em>点击上传</em>
    </div>
  </el-upload>
  <el-progress v-show="active === 1 && percentage >= 0" class="pt-20" :text-inside="true" :stroke-width="18" :percentage="percentage" status="success" />
  <p v-show="importStatus!== 0">导入状态：<span v-if="importStatus == 1" class="">文件导入成功！</span>
  <span v-else-if="importStatus == 2">文件导入失败！</span>
  </p>
</div>


<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'
import { cardImport } from '@/api/business/pysicalCard'
import { getToken } from '@/utils/cookies'
import dataImport from '@/components/ImportData/index.vue'
import { importExcel } from '@/utils/excelData'
import { fileData } from '@/api/excelData'

@Component({
  name: 'wristbandImport',
  components: {
    dataImport
  }
})
export default class extends Vue {
  private importPath = '/ticket/business/HandCard/Import'
  private active = 0
  private showFileList = false
  public percentage = 0 // 导入进度
  private size = 2 // 上传阀值
  public importStatus: number = 0 // 文件导入状态，0还没开始导入，1导入成功，2导入失败
  public importResult: Array<string> = [] // 导入结果
  handleRemove() {}
  handlePreview() {}

  /**
   * 上传文件，并处理数据，
   */
  importExcel(file: fileData) {
    // importPath 上传文件的接口
    importExcel(file, this, this.size, this.importPath)
  }
}
```

```
// 封装的通用方法
import { fileData, sheetData, vueInstance } from '@/api/excelData'
import { importExcelApi } from '@/api/common'
import { read, utils } from 'xlsx' // excel 处理插件

/** 读取excel数据
 * @param file 上传文件
 * @param that vue 实例
 * @param size 上传阀值
 * @param importPath 文件上传路径
 */
export function importExcel(file: fileData, that: vueInstance, size: number, importPath: string) {
  const types = file.name.split('.')[1]
  const fileType = ['xlsx', 'xlc', 'xlm', 'xls', 'xlt', 'xlw', 'csv'].some(item => item === types)
  if (!fileType) { // 上传文件类型判断
    that.$message({
      message: '上传格式不正确！仅支持xlsx,xlc,xlm,xls,xlt,xlw,csv等格式',
      type: 'warning'
    })
    return
  }
  file2Xce(file).then((tabJson: any) => {
    if (tabJson && tabJson.length > 0) {
      dealExcelData(tabJson, that, size, importPath)
    }
  })
}

/** 读取excel数据
 * @param file 上传文件
 */
export function file2Xce(file: fileData) {
  return new Promise(function(resolve, reject) {
    const reader = new FileReader()
    reader.onload = function(e: ProgressEvent) {
      const data = (e.target as FileReader).result
      const wb = read(data, {
        type: 'binary'
      })
      const result: Array<object> = []
      wb.SheetNames.forEach((sheetName) => {
        result.push({
          sheetName: sheetName,
          sheet: utils.sheet_to_json(wb.Sheets[sheetName])
        })
      })
      resolve(result)
    }
    reader.readAsBinaryString(file.raw)
  // reader.readAsBinaryString(file) // 传统input方法
  })
}

/** 处理excel数据
* @param excelData 单表sheet 数据
* @param  that vue 实例
* @param size 上传阀值
* @param importPath 文件上传路径
*/
export function dealExcelData(excelData: Array<sheetData>, that: vueInstance, size: number, importPath: string) {
  let allSheetData: Array<string> = []
  excelData.forEach((item: sheetData, index: number) => {
    if (item.sheet.length > 0) {
      allSheetData = allSheetData.concat(item.sheet)
    }
  })
  const page = 0
  const sheetLength = allSheetData.length
  const pageSize = Math.ceil(sheetLength / size)
  uploadExcelData(allSheetData, page, pageSize, sheetLength, that, importPath)
}

/** 上传excel数据
* @param uploadData 所有表sheet 数据
* @param page 当前上传第几页的数据
* @param pageSize 根据阀值划分的分页数（上传次数）
* @param that vue 实例
* @param size 上传阀值
* @param importPath 上传文件路径
*/
export async function uploadExcelData(uploadData: Array<string>, page: number, pageSize:number, size: number, that: vueInstance,
  importPath: string) {
  const uploadDataTemp = uploadData.splice(page * size, size)
  const param = {
    data: JSON.stringify(uploadDataTemp)
  }
  console.log('page=' + page + '  内容：' + uploadDataTemp)
  const { data } = await importExcelApi(importPath, param)
  if (data.code === 200) {
    that.importStatus = 1
    that.importResult = uploadDataTemp
    that.percentage = ((page + 1) / pageSize) * 100
    if (that.percentage < 100) {
      uploadExcelData(uploadData, page + 1, pageSize, size, that, importPath)
    }
  } else {
    that.importStatus = 2
  }
}

```
