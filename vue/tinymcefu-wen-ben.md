### tinymce富文本
tinymce-vue需购买tinymce的服务，所以直接下载tinymce
```
npm install tinymce
npm install --save @tinymce/tinymce-vue
```

#### [工具栏](http://tinymce.ax-z.cn/general/basic-setup.php#toolbarconfiguration)
* newdocument（新文档）
* bold（加粗）
* italic（斜体）
* underline（下划线）
* strikethrough（删除线）
* alignleft（左对齐）
* aligncenter（居中对齐）
* alignright（右对齐）
* alignjustify（两端对齐）
* styleselect（格式设置）
* formatselect（段落格式）
* fontselect（字体选择）
* fontsizeselect（字号选择）
* cut（剪切）
* copy（复制）
* paste（粘贴）
* bullist（项目列表UL）
* numlist（编号列表OL）
* outdent（减少缩进）
* indent（增加缩进）
* blockquote（引用）
* undo（撤销）
* redo（重做/重复）
* removeformat（清除格式）
* subscript（下角标）
* superscript（上角标）

#### 引入静态文件
* 将node_modules/tinymce/skins拷贝到public/tinymce目录下
* base_url: '/tinymce',  //"tinymce": "^5.3.2"需要
* 中文语言包 [下载地址](https://www.tiny.cloud/get-tiny/language-packages/)
* 支持图片复制上传:下载powerpaste [保留版本](/back-up/tinymce/powerpaste)
* 首行缩进，加载插件indent2em，[地址](http://tinymce.ax-z.cn/more-plugins/indent2em.php) ,和其他类似，新建index.js ```require('./plugin.js');```,然后在配置项的plugins和toolbar添加‘indent2em’
* 多图片上传：

  下载powerpaste [保留版本](/back-up/tinymce/powerpaste),新建index.js```require('./plugin.js');```
  
  修改plugin.js里的iframe1
  
  powerpaste中的upfiles.html、loading.gif放在public文件夹下
  
  配置项的plugins和toolbar添加‘axupimgs’
  
  images_upload_handler中blobInfo参数和单张图片上传会有所不一样 ```const name=typeof(blobInfo.filename)==='function'?blobInfo.filename():blobInfo.file.name```
  
  ![](/assets/tinymce.png)
  
 * 视频上传，加载插件media，[地址](http://tinymce.ax-z.cn/plugins/media.php)
 
   视频相关属性和方法：file_picker_types、video_template_callback、file_picker_callback
 
   富文本预览视频需要修改media源码：[5.3.2](/back-up/tinymce/5.3.2-media.js) [5.2.0](/back-up/tinymce/5.2.0-media.js)
  


#### 使用
```javascript
/* eslint-disable no-unused-vars */
import tinymce from 'tinymce'
// import  'tinymce'
import 'tinymce/themes/silver/theme'
import editor from '@tinymce/tinymce-vue'
import 'tinymce/plugins/image'
import 'tinymce/plugins/link'
import 'tinymce/plugins/lists'
import 'tinymce/plugins/textcolor'
import 'tinymce/plugins/colorpicker'
import 'tinymce/plugins/preview'
import 'tinymce/plugins/table'
import 'tinymce/plugins/indent2em'
import 'tinymce/plugins/lineheight'
import 'tinymce/plugins/axupimgs'
import 'tinymce/plugins/media'
import uploadFileApi from '../api/base/attach'
import {Loading} from 'element-ui';
import {config} from "@vue/test-utils";
import de from "element-ui/src/locale/lang/de";

const UPLOAD_URL = '/attach/public'

const EDITOR_CONFIG = {
    base_url: './tinymce',
    language_url: './tinymce/zh_CN.js',
    language: 'zh_CN',
    // skin_url: '/public/tinymce/skins/lightgray',
    skin_url: './tinymce/skins/ui/oxide',
    height: 600,
    plugins: 'link lists image table colorpicker textcolor preview indent2em lineheight axupimgs media',
    // plugins: 'link lists table colorpicker textcolor preview',
    external_plugins: {
        // 'powerpaste': '/tinymce/powerpaste/plugin.min.js' //复制图片相关
        'powerpaste': './powerpaste/plugin.min.js' //复制图片相关
    },
    menubar: false,
    // forced_root_block: 'wrap',
    forced_root_block: 'p',
    toolbar_mode: 'sliding',
    toolbar: `fontselect fontsizeselect lineheight | 
           bold italic underline strikethrough | 
           removeformat forecolor backcolor | 
           alignleft aligncenter alignright alignjustify | 
           bullist numlist | 
           indent2em outdent indent blockquote | 
           undo redo | 
           link unlink table image axupimgs media| 
           preview `,
    /*toolbar: 'code undo redo restoredraft | cut copy paste pastetext | forecolor backcolor bold italic underline strikethrough link anchor | alignleft aligncenter alignright alignjustify outdent indent | \
    styleselect formatselect fontselect fontsizeselect | bullist numlist | blockquote subscript superscript removeformat | \
    table image media charmap emoticons hr pagebreak insertdatetime print preview | fullscreen | bdmap indent2em lineheight formatpainter axupimgs',*/
    font_formats: `
          微软雅黑=Microsoft YaHei;
          宋体=SimSun;
          黑体=SimHei;
          仿宋=FangSong;
          楷体=KaiTi;
          隶书=LiSu;
          幼圆=YouYuan;`,
    fontsize_formats: '10px 11px 12px 14px 16px 18px 20px 22px 24px',
    branding: false, // 隐藏tinymce标记
    statusbar: false, // 隐藏编辑器底部的状态栏


    // CONFIG: Paste
    paste_retain_style_properties: 'all',
    paste_word_valid_elements: '*[*]', // 允许指定元素和属性保存在过滤结果中,word需要它
    paste_data_images: true, // 从粘贴的内容中删除data:url图像（内联图像）,粘贴的同时能把内容里的图片自动上传
    paste_convert_word_fake_lists: false, // 禁用复制word中的列表内容时，转换为html的UL或OL格式
    paste_webkit_styles: 'all', //指定在WebKit中粘贴时要保留的样式
    paste_merge_formats: true, //合并相似格式
    nonbreaking_force_tab: false,
    paste_auto_cleanup_on_paste: false,

    // CONFIG: ContentStyle 这块很重要， 在最后呈现的页面也要写入这个基本样式保证前后一致， `table`和`img`的问题基本就靠这个来填坑了
    content_style: `
    *                         { padding:0; margin:0; }
    html, body                { height:100%; }
    img                       { max-width:100%;}
    iframe                    { width: 100%; }
    p                         { margin: 0px;  }
    table                     { word-wrap:break-word; word-break:break-all; max-width:100%; border:none; border-color:#999; }
    .mce-object-iframe        { width:100%; box-sizing:border-box; margin:0; padding:0; }
    ul,ol                     { list-style-position:inside; }
    `,

    /*------------------------------------------- 图片相关 -------------------------------------------------*/
    relative_urls: false, //绝对路径
    images_upload_url: UPLOAD_URL, // 图片上传路径，不能删除，否则不能显示本地上传按钮
    // 自定义图片上传
    /* images_upload_handler: function (blobInfo, success, failure) {
         let formData = new FormData()
         // formData.append('file', blobInfo.blob())
         formData.append('upload', blobInfo.blob())
         formData.append('siteCode', this.websiteCode)
         uploadFileApi.add(formData).then((res) => {
                 success(res.data.url)
             }
         ).catch(() => {
             failure('发生错误,请稍后再试')
         })
     },*/

    // 粘贴前回调
    /*paste_preprocess:function (plugin, args) {
        console.log(plugin)
        console.log(args.content)
    }*/
    setup: function (ed) {
        /*ed.on('change', function () {
            ed.save()
        })*/
        ed.on('init', function () {
            this.execCommand("fontSize", false, "14px");
        });
    },

    /* -------------------------------------------------  上传文件相关 --------------------------------------- */
    file_picker_types: 'media',
    video_template_callback: function (data) {
        data.width = "100%";
        data.height = "auto";
        return `<p>
               <span class="mce-preview-object mce-object-video" contenteditable="false" 
               data-mce-object="video" data-mce-p-allowfullscreen="allowfullscreen" 
               data-mce-p-frameborder="no" data-mce-p-scrolling="no" 
               data-mce-p-src=${data.source} 
               data-mce-p-width=${data.width} 
               data-mce-p-height=${data.height} 
               data-mce-p-controls="controls" data-mce-html="%20">
                 <video width=${data.width} height=${data.height} controls="controls">
                  <source src=${data.source} type=${data.sourcemime}></source>
                 </video>
               </span>
            </p>`;
    },
    /*file_picker_callback: function (callback, value, meta) {
        if (meta.filetype == 'file') {
            callback('mypage.html', {text: 'My text'});
        }
        // Provide image and alt text for the image dialog
        if (meta.filetype == 'image') {
            callback('myimage.jpg', {alt: 'My alt text'});
        }
        // Provide alternative source and posted for the media dialog
        if (meta.filetype == 'media') {
            callback('movie.mp4', {source2: 'alt.ogg', poster: 'image.jpg'});
        }
    }*/
}

export default {
    mixins: [],
    extends: {},
    props: {
        websiteCode: {
            type: String
        }
    },
    data () {
        return {
            linkList: [
                {
                    name: '是',
                    value: 1
                },
                {
                    name: '否',
                    value: 0
                }
            ],
            editorInit: null
        }
    },
    computed: {},
    components: {
        editor
    },
    watch: {},
    methods: {
        initEditor () {
            const websiteCode = this.websiteCode

            EDITOR_CONFIG.images_upload_handler = function (blobInfo, success, failure) {
                let formData = new FormData()
                const name = typeof (blobInfo.filename) === 'function' ? blobInfo.filename() : blobInfo.file.name
                formData.append('upload', blobInfo.blob(), name)
                formData.append('siteCode', websiteCode)
                uploadFileApi.add(formData).then((res) => {
                    success(res.data.url)
                }).catch(() => {
                    failure('发生错误,请稍后再试')
                })
            }
            EDITOR_CONFIG.file_picker_callback = function (callback, value, meta) {
                const filetype = 'video/*'
                //模拟出一个input用于添加本地文件
                let input = document.createElement('input')
                input.setAttribute('type', 'file')
                input.setAttribute('accept', filetype)
                input.click()
                input.onchange = function () {
                    let loading = Loading.service({
                        lock: true,
                        text: '正在上传',
                        spinner: 'el-icon-loading',
                        background: 'rgba(0, 0, 0, 0.7)'
                    })
                    const file = this.files[0]
                    let formData = new FormData()
                    formData.append('upload', file, file.name)
                    formData.append('siteCode', websiteCode)
                    uploadFileApi.add(formData, {
                        onUploadProgress:(progressEvent) => {
                            let rate = (progressEvent.loaded / progressEvent.total * 100 | 0)
                            rate=rate===100?99:rate
                            const uploadMessage = '正在上传 ' + rate + '%'
                            loading.text=uploadMessage
                        }
                    }).then((res) => {
                        callback(res.data.url)
                    }).catch(() => {
                    }).finally(() => {
                        loading.close()
                    })
                }
            }
            this.editorInit = EDITOR_CONFIG
        }
    },
    beforeCreate () {
    },
    mounted () {
        this.initEditor()
    }
}

// 备份
/*
*  font_formats: `
          微软雅黑=微软雅黑;
          宋体=宋体;
          黑体=黑体;
          仿宋=仿宋;
          楷体=楷体;
          隶书=隶书;
          幼圆=幼圆;
          Andale Mono=andale mono,times;
          Arial=arial, helvetica,
          sans-serif;
          Arial Black=arial black, avant garde;
          Book Antiqua=book antiqua,palatino;
          Comic Sans MS=comic sans ms,sans-serif;
          Courier New=courier new,courier;
          Georgia=georgia,palatino;
          Helvetica=helvetica;
          Impact=impact,chicago;
          Symbol=symbol;
          Tahoma=tahoma,arial,helvetica,sans-serif;
          Terminal=terminal,monaco;
          Times New Roman=times new roman,times;
          Trebuchet MS=trebuchet ms,geneva;
          Verdana=verdana,geneva;
          Webdings=webdings;
          Wingdings=wingdings,zapf dingbats`,
* */

```

```
 <editor v-model="article.content" :init="editorInit"></editor>
```



