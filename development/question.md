<!-- 项目大标题 -->
<h1 align="center">开发常见问题</h1>
<!-- 文档说明 -->
开发中常见问题大家随时记录下来，以避免后期再次遇到同样的问题<br/>
😋💕🦄

## 开发标准
##### 1、脚手架里没用的代码和文件，一定要去掉
##### 2、本地开发的时候，要让编辑后的代码，0报错，0警告
##### 3、尽量避免用各种插件，能自己写的就自己写，jquery插件除外
- 有些插件对老版本浏览器兼容不好，万一到时不兼容，还得改
- 插件会增大项目体积，造成打出来的包也会很大


## Tizen浏览器版本兼容问题
主要说明由于Tizen浏览器4.0和5.0之间的兼容性问题造成的不兼容问题
#### 1、getBoundingClientRect问题
div.getBoundingClientRect()可以获取
* Tizen4.0：width、height、top、right、bottom、left
* Tizen5.0：width、height、top、right、bottom、left、x、y

```javascript
let clientRect = currentRect.getBoundingClientRect();
if (clientRect.x === undefined || clientRect.x === '') {
    // 检测到没有x的情况下，将left、top赋值给x、y
    clientRect = {
        x: clientRect.left ? clientRect.left : currentRect.offsetLeft,
        y: clientRect.top ? clientRect.top : currentRect.offsetTop,
        width: clientRect.width ? clientRect.width : currentRect.clientWidth,
        height: clientRect.height ? clientRect.height : currentRect.clientHeight,
        top: clientRect.top ? clientRect.top : currentRect.offsetTop,
        left: clientRect.left ? clientRect.left : currentRect.offsetLeft,
        right: clientRect.right ? clientRect.right : currentRect.offsetLeft + currentRect.clientWidth,
        bottom: clientRect.bottom ? clientRect.bottom : currentRect.offsetTop + currentRect.clientHeight
    };
}
```
#### 2、flex在老版本中UI问题
- 由于react在编译过程会将flex的兼容写法过滤掉，所以我们在public中单独引用flex样式文件./public/css/flex.css（免去编译的步骤，保留原汁原味代码）
- 在项目中的组件样式中，严谨使用flex样式，如果使用的话，将样式名字放到./public/flex.css中
- 项目中严禁使用display: inline-flex;  老版本不兼容

#### 3、老版本的js兼容问题，通过babel-polyfill来解决，具体解决方式如下
```javascript
// 在./config/webpack.config.js中增加babel-polyfill
entry: [
    'babel-polyfill',
    // -- 其他自有配置    
].filter(Boolean)
```


## 开发问题

#### 1、变量赋值
- 全局变量赋值请使用**var**，let赋值后在个别机型会出现undefined。
#### 2、config.xml文件
- 新建项目之后，请将旧项目的引入都复制过来，否则将使个别机型的播放器不能播放视频。
- `<name>XXX</name>` 标签中的XXX可以使中文，这是APP的名字。
- `<tizen:application id="XXXX.xxx" package="XXXX" required_version="2.3"/>` 这个标签是新建项目生成的唯一ID，之后上传到三星那边将作为唯一标识，如果出现差异会造成上传失败。
- `<widget></widget>` 标签的属性**version**是APP的版本号，每次上传到三星之前（包括修改BUG之后的上传）请变更版本号。
#### 3、cookie使用
- cookie在模拟器不可使用，在个别型号真机也有问题，所以尽量使用localStorage。
#### 4、播放器
- 如果将播放器元素赋值到全局变量后，离开页面请置空或清除该变量，否则会有别的页面后台运行该播放器。
- 播放器绑定JS操作事件 如 onplaying 等，个别机型只有第一次执行。
- 进度条需要自定义。
- 播放器的父元素如果使用overflow:hidden,在个别机型会造成播放器黑屏。
#### 5、网络接口的使用
- 所有接口访问的数据，都进行错误判断，如果发生获取错误主动重复访问3次，都不行再弹出访问错误（可以参考唱吧项目：https://github.com/aishuda/changba）