<h1 align="center">Tiezn Studio 前端开发注意事项</h1>

一些开发过程中踩过的坑和Tizen的使用建议

## 环境

Tizen Studio 是三星自己的开发工具，我们可以不使用他的IDE来编辑代码，但是要用他来将项目打包，才能使得三星认同

### 安装

* 安装包下载地址： [下载Tizen Studio](https://developer.tizen.org/development/tizen-studio/download)

建议安装到C盘你找得到的地方（该程序不生成桌面快捷方式）

安装完成后运行 tizen-studio/ide/TizenStudio.exe (为了方便后续使用，建议生成桌面快捷方式)

### 插件

我们开发的电视APP需要对应的开发环境，下面的插件就是电视的开发环境了

第一步：打开插件安装器

![](../image/插件安装_1.png)

第二步：下载本地测试机插件

![](../image/插件安装_2.jpg)

第三步：下载扩展插件

![](../image/插件安装_3.jpg)

插件下载完之后就可以运行测试环境了(右键点击你的项目)

![](../image/测试机环境运行.jpg)

### 数字证书

真机测试就需要将你的项目用Tizen Studio打包了，打包需要对应的数字证书，下面就是数字证书的安装了

第一步：打开数字证书安装

![](../image/数字证书_1.jpg)

第二步：新建数字证书

![](../image/数字证书_2.jpg)