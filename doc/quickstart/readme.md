# 五分钟快速上手
我们的快速上手的目标是：用TypeScript构建并运行一个超级简单Angular2应用

## 下载源码
急着上手？[下载](https://github.com/angular/quickstart/blob/master/README.md)本快速上手的源码然后开始Coding吧

## 看它运行起来
试试这个[plunker](http://plnkr.co/)上的[在线例子](https://angular.io/resources/live-examples/quickstart/ts/plnkr.html)，它显示了一些简单的信息：  
![first Angular2 App](../../res/img/my-first-app.png)

## 学习
当然，我们不是为了在plunker上运行而去构建应用。下列是建立本文档所有例子所使用的开发环境，这也可以是真正生产环境的基础。首先，我们将要：
* 准备[开发环境](开发环境)
* 编写应用的Angular[根组件](根组件)
* 编写告诉Angular如何展示根组件的[main.ts](main.ts)文件
* 编写[承载网页](承载网页)（index.html）

```
在我们展开这个话题的时候，我们会看到很多代码块。他们都很可以很容易的被复制和粘贴。
```

## 开发环境
我们需要准备我们的开发环境：
* 安装node和npm
* 创建[应用项目文件夹](项目文件夹)
* 添加指导TypeScript编译器所需的[tsconfig.json](tsconfig.json)
* 添加[typings.json](typings.json)用来定位无法找到的TypeScript定义文件
* 添加[package.json](package.json)用来定义我们需要用到的包和脚本
* 安装npm包和typings文件

如果你的机器上没有**node和npm 请[安装](https://nodejs.org/en/download/)**

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

### **通过*npm*添加我们需要的库**
Angular应用开发者依赖*[npm](https://docs.npmjs.com/)*包管理器来安装应用所需的库。Angular团队推荐定义在`dependencies`和`devDependencies `中的入门套件包。在[npm包](./doc/develop-guide/npm-packages/readme.md)章节中查看详细信息。
### **帮助性脚本**
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
