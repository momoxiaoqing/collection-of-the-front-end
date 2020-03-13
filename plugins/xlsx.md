### XLSX

 #### 接口返回stream显示excel文件内容
 ```
 fileInterface().then((res) => {
      let reader = new FileReader()
      reader.onload = e => {
          let data = e.target.result
          const workbook = XLSX.read(data, {type: 'array'})
          workbook.SheetNames.forEach(sheetName=>{
              this.tableDomList.push({
                  sheetName:sheetName,
                  content:XLSX.utils.sheet_to_html(workbook.Sheets[sheetName])
              })
          })
      }
      reader.readAsArrayBuffer(res.data)
  }).catch(() => {
  })
 ```

 #### stream 转json
 ```
 let reader = new FileReader()
 reader.onload = e => {
     const res = JSON.parse(e.target.result)
     ...
 }
 reader.readAsText(response.data)
 ```
