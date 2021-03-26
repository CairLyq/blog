
## 注意事项
1. exml 文件中禁止使用多状态，用代码描述状态。
2. class 不要使用 默认导出  `export default class`
3. model 不参与业务逻辑，只做数据存储容器
4. viewModel 处理业务逻辑以及提供数据给 UIView 使用
5. 创建皮肤要加 skins 前缀
6. number 类型要改用 int , 明确是小数的用 float
7. 坐标类型: IVec2 , IVec2Like   坐标实体: Vec2
8. 常量用 const 定义 ,变量用 let
9. 通用的接口添加到 interface.ts
10. 编辑 i18n 文件时上锁 getLock , 提交之后会自动释放锁.  
锁住状态表示有人在编辑,等待锁释放之后再进行编辑.
11. ViewModel 中尽量少存变量，提供方法给外部使用，变量需要在 init 方法中重置。





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



## src 文件夹释义

- adapter                                   资源加载适配器
- component                                 通用组件
- data                                      常量及配表
- extension                                 引擎扩展
- module                                    子模块
- scene                                     场景
- sound                                     音效
- utils                                     工具类
- viewstrategy                              UI 策略
- debug.ts                                  debug
- interface.ts                              通用接口定义
- Main.ts                                   程序入口


## aplay 文件夹释义

- data                                      配置,常量数据读取
- logic                                     战斗演算逻辑
- raid                                      副本,PVP数据
- round                                     回合状态以及回合动作
- state                                     状态机
- unit                                      角色以及其他实体单位
- Action.ts                                 龙骨动作
- BattleMgr.ts                              全局战斗管理
- FlutterMgr.ts                             战斗飘字管理
- GameStateMgr.ts                           全局游戏状态机
- UnitMgr.ts                                单位管理,创建以及回收单位
- World.ts                                  世界实体渲染,每帧更新实体












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










### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/CairLyq/cair.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
