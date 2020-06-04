#### 文件下载
```
 const blob = new Blob([res.data], {type: 'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet;charset=utf-8'});
 //从response的headers中获取filename, 后端response.setHeader("Content-disposition", "attachment; filename=xxxx.docx") 设置的文件名;
 const contentDisposition = res.headers['content-disposition'];
 const patt = new RegExp("filename=([^;]+\\.[^\\.;]+);*");
 const result = patt.exec(contentDisposition);
 const fileName = decodeURI(result[1]);
 if ('download' in document.createElement('a')) { //非IE下载
     const downloadElement = docum ent.createElement('a');
     const href = window.URL.createObjectURL(blob); //创建下载的链接
     downloadElement.style.display = 'none';
     downloadElement.href = href;
     downloadElement.download = fileName;
     document.body.appendChild(downloadElement);
     downloadElement.click();
     document.body.removeChild(downloadElement);
     window.URL.revokeObjectURL(href);
 } else { //IE10+下载
     navigator.msSaveBlob(blob, fileName)
 }
```