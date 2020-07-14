### tinymce富文本
tinymce-vue需购买tinymce的服务，所以直接下载tinymce
```
npm install tinymce
npm install --save @tinymce/tinymce-vue
```

#### 引入静态文件
* 将node_modules/tinymce/skins拷贝到public/tinymce目录下
* base_url: '/tinymce',  //"tinymce": "^5.3.2"需要
* 中文语言包 [下载地址](https://www.tiny.cloud/get-tiny/language-packages/)
* 支持图片复制上传:下载powerpaste [保留版本](/plugins/powerpaste)
* 首行缩进，加载插件indent2em，[地址](http://tinymce.ax-z.cn/more-plugins/indent2em.php),和其他类似，新建index.js ```require('./plugin.js');```,然后在配置项的plugins和toolbar添加‘indent2em’


![](/assets/tinymce.png)

#### 使用
```
/* eslint-disable no-unused-vars */
import tinymce from 'tinymce'
import 'tinymce/themes/silver/theme'
import editor from '@tinymce/tinymce-vue'
import 'tinymce/plugins/image'
import 'tinymce/plugins/link'
import 'tinymce/plugins/lists'
import 'tinymce/plugins/textcolor'
import 'tinymce/plugins/colorpicker'
import 'tinymce/plugins/preview'
import 'tinymce/plugins/table'
import uploadFileApi from '../api/upload-file'

const UPLOAD_URL = 'uploadFile'

const EDITOR_CONFIG = {
    language_url: '/tinymce/zh_CN.js',
    language: 'zh_CN',
    // skin_url: '/public/tinymce/skins/lightgray',
    skin_url: '/tinymce/skins/ui/oxide',
    height: 300,
    plugins: 'link lists image table colorpicker textcolor preview',
    // plugins: 'link lists table colorpicker textcolor preview',
    external_plugins: {
        'powerpaste': '/tinymce/powerpaste/plugin.min.js' //复制图片相关
    },
    menubar: false,
    forced_root_block: 'p',
    toolbar: `formatselect fontsizeselect |
           bold italic underline strikethrough |
           forecolor backcolor |
           alignleft aligncenter alignright alignjustify |
           bullist numlist |
           outdent indent blockquote |
           undo redo |
           link unlink table image |
           removeformat preview `,
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
    paste_word_valid_elements: '*[*]', // word需要它
    paste_data_images: true, // 粘贴的同时能把内容里的图片自动上传，但Chrome中无效
    paste_convert_word_fake_lists: false, // 插入word文档需要该属性
    paste_webkit_styles: 'all',
    paste_merge_formats: true,
    nonbreaking_force_tab: false,
    paste_auto_cleanup_on_paste: false,

    // CONFIG: ContentStyle 这块很重要， 在最后呈现的页面也要写入这个基本样式保证前后一致， `table`和`img`的问题基本就靠这个来填坑了
    content_style: `
    *                         { padding:0; margin:0; }
    html, body                { height:100%; }
    img                       { max-width:100%;}
    a                         { text-decoration: none; }
    iframe                    { width: 100%; }
    p                         { margin: 0px;  }
    table                     { word-wrap:break-word; word-break:break-all; max-width:100%; border:none; border-color:#999; }
    .mce-object-iframe        { width:100%; box-sizing:border-box; margin:0; padding:0; }
    ul,ol                     { list-style-position:inside; }
    `,
    images_upload_url: UPLOAD_URL, // 图片上传路径，不能删除，否则不能显示本地上传按钮
    // 自定义图片上传
    images_upload_handler: function (blobInfo, success, failure) {
        let formData = new FormData()
        formData.append('file', blobInfo.blob(),blobInfo.filename())
        uploadFileApi.add(formData).then((res) => {
                success(res.data.url)
            }
        ).catch(() => {
            failure('发生错误,请稍后再试')
        })
    }
    /* setup: function (editor) {
      editor.on('change', function () {
        editor.save()
      })
    } */
}

export default {
    mixins: [],
    extends: {},
    props: {},
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
            editorInit: EDITOR_CONFIG
        }
    },
    computed: {},
    components: {
        editor
    },
    watch: {},
    methods: {
    },
    beforeCreate () {
    },
    mounted () {
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
