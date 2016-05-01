# 五分钟快速上手
我们的快速上手的目标是：用TypeScript构建并运行一个超级简单Angular2应用

## 下载源码
急着上手？[下载](https://github.com/angular/quickstart/blob/master/README.md)本快速上手的源码然后开始Coding吧

## 查看实例
试试这个[plunker](http://plnkr.co/)上的[在线例子](https://angular.io/resources/live-examples/quickstart/ts/plnkr.html)，它显示了一些简单的信息：  
![first Angular2 App](../../res/img/my-first-app.png)

## 学习
当然，我们不是为了在plunker上运行而去构建应用。下列是建立本文档所有例子所使用的开发环境，这也可以是真正生产环境的基础。首先，我们将要：
* 准备[开发环境](#开发环境)
* 编写应用的Angular[根组件](#根组件)
* 编写告诉Angular如何展示根组件的[main.ts](#main.ts)文件
* 编写[承载网页](#承载网页)（index.html）

```
在我们展开这个话题的时候，我们会看到很多代码块。他们都很可以很容易的被复制和粘贴。
```

### 开发环境
我们需要准备我们的开发环境：
* 安装node和npm
* 创建[应用项目文件夹](#应用项目文件夹)
* 添加指导TypeScript编译器所需的[tsconfig.json](#tsconfig.json)
* 添加[typings.json](#typings.json)用来定位无法找到的TypeScript定义文件
* 添加[package.json](#package.json)用来定义我们需要用到的包和脚本
* 安装npm包和typings文件

如果你的机器上没有**node和npm 请[安装](https://nodejs.org/en/download/)**
<p id="应用项目文件夹"></p>
创建一个**新的项目文件夹**
```batch
mkdir angular2-quickstart
cd    angular2-quickstart
```
在项目文件夹中添加**tsconfig.json**文件并复制粘贴下面的内容：
```json
{
  "compilerOptions": {
    "target": "es5",
    "module": "system",
    "moduleResolution": "node",
    "sourceMap": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "removeComments": false,
    "noImplicitAny": false
  },
  "exclude": [
    "node_modules",
    "typings/main",
    "typings/main.d.ts"
  ]
}
```
`tsconfig.json`文件用来引导TypeScript编译器。在[TypeScript配置](./doc/develop-guide/typescript-configuration/readme.md)章节中可以了解到更多。  

在项目文件夹中添加**typings.json**文件并复制粘贴下面的内容：
```json
{
  "ambientDependencies": {
    "es6-shim": "registry:dt/es6-shim#0.31.2+20160317120654",
    "jasmine": "registry:dt/jasmine#2.2.0+20160412134438"
  }
}
```
> 许多JavaScript库用特性和语法扩展了JavaScript环境，这些是TypeScript编译器无法本地识别的。
> 我们通过定义在`typings.json`文件中的TypeScript类型定义文件—*.d.ts文件*来告诉TypeScript这些扩展功能。

在项目文件夹中添加**package.json**文件并复制粘贴下面的内容：
```json
{
  "name": "angular2-quickstart",
  "version": "1.0.0",
  "scripts": {
    "start": "tsc && concurrently \"npm run tsc:w\" \"npm run lite\" ",
    "lite": "lite-server",
    "postinstall": "typings install",
    "tsc": "tsc",
    "tsc:w": "tsc -w",
    "typings": "typings"
  },
  "license": "ISC",
  "dependencies": {
    "angular2": "2.0.0-beta.17",
    "systemjs": "0.19.26",
    "es6-shim": "^0.35.0",
    "reflect-metadata": "0.1.2",
    "rxjs": "5.0.0-beta.6",
    "zone.js": "0.6.12"
  },
  "devDependencies": {
    "concurrently": "^2.0.0",
    "lite-server": "^2.2.0",
    "typescript": "^1.8.10",
    "typings":"^0.8.1"
  }
}
```

#### **通过*npm*添加我们需要的库**
Angular应用开发者依赖*[npm](https://docs.npmjs.com/)*包管理器来安装应用所需的库。Angular团队推荐定义在`dependencies`和`devDependencies `中的入门套件包。在[npm包](./doc/develop-guide/npm-packages/readme.md)章节中查看详细信息。
#### **帮助性脚本**
我们在推荐的`package.json`文件中包含了许多npm脚本以应对常规的开发任务：
```json
{
  "scripts": {
    "start": "tsc && concurrently \"npm run tsc:w\" \"npm run lite\" ",
    "lite": "lite-server",
    "postinstall": "typings install",
    "tsc": "tsc",
    "tsc:w": "tsc -w",
    "typings": "typings"
  }
}
```
我们通过以下方式执行大多数npm脚本：`npm run`+*脚本名*。有些命令（如`start`）不需要`run`关键字。  
这些脚本做了这些事情：
* `npm start` - 同时使用监视模式启动编译器和服务器
* `npm run tsc` - 运行一次TypeScript编译器
* `npm run tsc:w` - 使用监视模式运行TypeScript编译器；这个进程始终运行并实时编译TypeScript文件的改动
* `npm run lite` - 启动[lite-server](https://www.npmjs.com/package/lite-server)，一个拥有对使用路由的Angular应用有很棒支持的轻量级静态文件服务器
* `npm run typings` - 启动[typings工具](#typings工具)
* `npm run postinsall` - 在*npm*成功完成安装包*之后*自动被调用，这个脚本安装定义在`typings.json`文件中的[TypeScript定义文件](#typings)

通过在终端窗口（Windows中的命令窗口）输入以下*npm*命令来安装这些包
```batch
npm install
```

> 安装**过程中**会出现吓人的<span style="color:red;">**红色报错信息**</span>。安装过程通常可以从这些错误中恢复并成功完成。  
> 
> **npm错误和警告**
> 
> 如果**npm insall**结束后没有任何以`npm ERR!`开头的控制台信息，那么一切顺利。一些`npm WARN`信息可能会出现，不过不要担心。
> 
> 我们经常可以在一系列`gyp ERR!`之后看到一个`npm WARN`信息。忽略他们吧。包可能会尝试使用`node-gyp`重新编译自己。如果重新编译失败，那么这个包将会恢复（通常使用预编译好的版本）然后所有人正常工作。
> 
> 只要确保在`npm install`结束后没有`npm ERR!`就行了。

**我们已经都准备好了。**让我们写一些代码吧。

### 第一个Angular组件
创建一个承载应用的文件夹并添加一个超级简单的Angular组件。
在根路径下**创建*app*子文件夹**并设置为当前路径
```batch
mkdir app
cd    app
```
创建名为*app.component.ts*的**组件文件**并粘贴下面的代码：
```typescript
import {Component} from 'angular2/core';

@Component({
    selector: 'my-app',
    template: '<h1>My First Angular 2 App</h1>'
})
export class AppComponent { }
```

#### **AppComponent是应用的入口**
每一个Angular应用都只要有一个根组件，为了方便我们把他命名为`AppComponent`，它承载了客户端的用户体验。  
组件是Angular应用的基本组成部分。组件通过它关联的模板控制屏幕的一部分—*视图*。  
这个快速上手只有一个超级简单的组件。但是它拥有每一个我们将会编写的组件的必备结构：
* 一个或多个`import`语句用来引用我们所需的东西
* `@Component装饰器`用来告诉Angular应该使用什么模板以及怎么创建这个组件
* `component类`通过模板控制视图的表现和行为

#### **导入**
Angular应用是模块化的。它由许多都专注于单一目的的文件组成。  
Angular本身也是模块化的。他是许多库模块的集合，我们在构建应用时将会用到许多相关的特性。