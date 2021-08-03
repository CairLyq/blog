# blog
新手上路指引

## 注意事项
1. exml 文件中禁止使用多状态，用代码描述状态。
2. class 不要使用 默认导出  `export default class`
3. model 不参与业务逻辑，只做数据存储容器
4. viewModel 处理业务逻辑以及提供数据给 UIView 使用
5. 创建皮肤要加 skins 前缀
6. number 类型要改用 int , 明确是小数的用 float
7. 坐标类型: IVec2 , IVec2Like   坐标实体: Vec2
8. 常量用 const 定义 ,变量用 let


### 开发日志
- 2021/03/26  
引擎升级到 5.4.1 版本 需要更改 源码 eui.Group $hitTest() ,
[eui.UILayer 的 touchEnabled 属性在 5.4.1 对比 5.4.0 版本有什么变化](https://bbs.egret.com/thread-60744-1-1.html)
```
$hitTest(stageX: number, stageY: number): egret.DisplayObject {
            let target = super.$hitTest(stageX, stageY);
            if (target || this.$Group[Keys.touchThrough]) {
                return target;
            }

            //Bug: 当 group.sacleX or scaleY ==0 的时候，随便点击那里都点击成功
            //虽然 super.$hitTest里面检测过一次 宽高大小，但是没有直接退出这个函数，所以要再判断一次;
            if (!this.$visible || !this.touchEnabled || this.scaleX === 0 || this.scaleY === 0 || this.width === 0 || this.height === 0) {
                return null;
            }
            let point = this.globalToLocal(stageX, stageY, egret.$TempPoint);
            let values = this.$UIComponent;
            let bounds = egret.$TempRectangle.setTo(0, 0, values[sys.UIKeys.width], values[sys.UIKeys.height]);
            let scrollRect = this.$scrollRect;
            if (scrollRect) {
                bounds.x = scrollRect.x;
                bounds.y = scrollRect.y;
            }
            if (bounds.contains(point.x, point.y)) {
                return this;
            }
            return null;
        }
```




## 位操作
```
// 取模 &
value % 2 ==> value  & 1;

// 取整 ~~
~~10.12 = 10
~~10    = 10
~~'1.5' = 1
~~undefined = 0
~~null  = 0

// 位掩码

const a = 1, b = 2,c = 4;
const options = a | b | c

// b 是否在选项中
if( b & options){
    
}

```

