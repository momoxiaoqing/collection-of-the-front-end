### git 常用操作

#### 查看地址
`git remote -v`

#### 删除已追踪文件
删除.idea文件
`git rm -r --cached .idea/ `

#### reset操作
* soft：已add缓存不变，回退commit信息，本地文件不变
* mixed：已add缓存丢失，回退commit和index信息，本地文件不变
* hard：彻底回退，本地文件不保留修改，但是未add的文件不变

#### 切换分支
```
git branch -a    //查看全部分支（含远程）
git branch      //查看本地分支
git checkout master   //切换到master分支
```