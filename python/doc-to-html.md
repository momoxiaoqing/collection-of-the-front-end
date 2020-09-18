### doc批量转docx，docx批量转html
```
import json
import os
import re
import win32com.client

from pydocx import PyDocX

work_dir = r'D:\文档-项目\白沙洲\企业'
from_dir = os.path.join(work_dir, '企业资料-整理')
to_dir = os.path.join(work_dir, '企业资料-html')
print(from_dir)

menu = {}

# python -c 'import docx2html; docx2html.f1()'
def toDocx():
    w = win32com.client.Dispatch('Word.Application')
    for file_name in os.listdir(from_dir):
        name_split = file_name.split('.')
        file_type=name_split[-1]
        new_file_name=file_name

        is_need_rename='简介' in file_name or ' ' in file_name
        if is_need_rename:
            new_file_name=new_file_name.replace(' ','')
            start_index= new_file_name.find('简介')
            new_file_name=new_file_name[0:start_index]+'.'+name_split[-1]
            os.rename(os.path.join(from_dir, file_name),os.path.join(from_dir, new_file_name))
            #print(file_name+'---->'+new_file_name)

        name_split = new_file_name.split('.')
        if file_type=='doc':
            docx_name=name_split[0]+'.docx'
            doc=w.Documents.Open(os.path.join(from_dir, new_file_name))
            doc.SaveAs(os.path.join(from_dir, docx_name),16) #必须有参数16，否则会出错.
            doc.Close()
            os.remove(os.path.join(from_dir,new_file_name))
            print(file_name+'---->'+docx_name)
        else:
            print(file_name+'---->'+new_file_name)

def toHtml():
    for ind,docx_name in enumerate(os.listdir(from_dir)):
        name_split = docx_name.split('.')
        corp_name= name_split[0]
        index=ind+1
        html_name = '%s-%s.html' % (index, corp_name)

        # 放入索引
        #corp_index[index] = corp_name
        #docx_path = os.path.join(from_dir, docx_name)
        #html_path = os.path.join(to_dir, html_name)
        #print('%s --> %s' % (docx_path, html_path))
        #html = PyDocX.to_html(docx_path)

        # 放入json
        corp_name=corp_name.split('-产品')[0]
        if menu.get(corp_name) is None:
            menu[corp_name] = {
                "index": index
            }
        if '-产品.' in html_name:
            menu[corp_name]["product"] = html_name
        else:
            menu[corp_name]["introduce"] = html_name

        docx_path = os.path.join(from_dir, docx_name)
        html_path = os.path.join(to_dir, html_name)
        print('%s --> %s' % (docx_path, html_path))

        html = PyDocX.to_html(docx_path)
        with open(html_path, 'w', encoding='utf-8') as html_file:
            html_file.write(html)
            html_file.close()

    # 保存索引
    with open(os.path.join(to_dir, 'menu.json'), 'w', encoding='utf-8') as menu_file:
        str_json = json.dumps(menu, ensure_ascii=False, sort_keys=True, indent=2)
        menu_file.write(str_json)
        menu_file.close()
```