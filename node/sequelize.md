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

### $like，分页

```js
 typeModel.findAll({
            where: {
                 name:{
                     $like: '%aaa%'
                 }，
                 limit：20,  //查20条记录
                 offset：0   //从第0条记录开始查
            }
        })
```



### 格式化时间

```js
var Article = sequelize.define('article',{
    id:{ type: Sequelize.INTEGER, primaryKey: true},
    publishTime:{type:Sequelize.DATE,field:'publish_time',
         /*
         用这种方法，update时会报错
          get: function () {
            return this.getDataValue('publishTime').toISOString().slice(0, 10);
        }
        */
        //需引入moment
        get:function () {
            return moment.utc(this.getDataValue('publishTime')).format('YYYY-MM-DD');
        }
    }
},{
    freezeTableName: true,//不修改表名为复数
    timestamps: false//不自动添加时间搓
})
```



