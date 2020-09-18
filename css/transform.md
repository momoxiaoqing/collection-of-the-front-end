### css动画相关
* transform
* transform-origin // 更改一个元素变形的原点，默认是元素中心


#### transform
兼容性：IE10+

|  函数   |  说明  |  类似属性 |   备注 |
|  ----   | ----  |  ----    | ----  |
| matrix(a, b, c, d, tx, ty)  | 转化函数 | matrix3d(...)  |  |
| translate(tx, [ty])  | 位移 | translate3d(tx, ty, tz) <br> translateX(t) <br> translateY(t) <br> translateZ(t) |  |
| rotate3d(x, y, z, a)   | 旋转变换，默认当前元素坐标系原点，原点由 transform-origin指定 | rotateX(a) <br> rotateY(a) <br> rotateZ(a)| x、y、z分别表示旋转轴向量的坐标 |
| scale(sx, [sy])  | 缩放，sy默认值为sx  | scale3d(sx, sy, sz) <br> scaleX(s) <br> scaleY(s) <br> scaleZ(s)|  | 
| skew(ax, [ay])  | 拉伸  | skewX(a) <br> skewY(a)|  | 
| perspective(l)  | z=0平面与用户之间的距离 |   |带px |

#### transition
语法:`\transition: property duration timing-function delay;`

兼容性：IE10+

* transition-property：指定CSS属性的name，
* transition-duration：效果需要指定多少秒或毫秒才能完成
* transition-timing-function：转速曲线
* transition-delay：定义效果开始的时候

