### element-ui

#### el-upload 图片列表显示闪现问题
若用file-list显示图片列表，file-list需要在uploadSuccess中手动赋值
```vue
<template>
    <el-upload class="g-upload-div"
               action=""
               :multiple="true"
               :on-remove="handleRemove"
               :file-list="imgList"
               list-type="picture-card"
               :data="{type:'imgList'}"
               :show-file-list="true"
               accept="image/*"
               :before-upload="beforeUpload"
               :http-request="upload"
               :on-success="uploadSuccess">
        <i class="el-icon-plus"></i>
        <!-- <div class="el-upload__text">将文件拖到此处，或<em>点击上传</em></div>
         <div class="el-upload__tip" slot="tip">只能上传图片，且不超过10MB</div>-->
    </el-upload>
</template>


<script>
    export default {
        methods:{
            handleRemove (file, fileList) {
                this.imgList = fileList
            },
            uploadSuccess (response, file, fileList) {
                file.id = response.id
                this[response.key] = fileList
            },
            upload (params) {
                const loding = this.$loading({
                    lock: true,
                    text: '正在上传中',
                    spinner: 'el-icon-loading',
                    background: 'rgba(0, 0, 0, 0.7)'
                })
        
                let form = new FormData()
                form.append('uploadFile', params.file)
                uploadFileApi.add(form).then((res) => {
                    // 调用uploadSuccess
                    params.onSuccess({
                        id: res.data.id,
                        key: 'imgList'
                    })
                    loding.close()
                }).catch(() => {
                    loding.close()
                })
            },
            beforeUpload (file) {
                const size = file.size
                if (size / 1024 / 1024 >= 1) {
                    this.$confirm('图片超过10MB，无法上传?', '图片过大', {
                        confirmButtonText: '确定',
                        // cancelButtonText: '继续上传',
                        type: 'warning'
                    }).then(() => {
                    }).catch(() => {
                    })
                    return false
                }
            }
        }
    }
</script>
```