### 排序：

```js
Sequelize.findAll({
            where: {...},
            order: [
                /*['sortNum', 'DESC']*/
                 ['sortNum', 'ASC']
            ]
        })
```



### update

```js
 //单条update
 typeModel.findById(id)
            .then(function (result){
                 result.status = 0
                    result.save();
            })
 //批量update
   typeModel.update(
                {status: 0}, //update的内容
                {where:{id:[1,2,3]}}  //update项的条件
                ).spread((affectedCount, affectedRows)=>{
                ......
            });
```



