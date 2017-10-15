## babel-register
`babel-register`模块改写`require`命令，为它加上一个钩子。此后，每当使用`require`加载`.js`、`.jsx`、'.es'和`.es6`后缀名的文件，就会先使用Babel进行转码。
`npm i -D babel-register`
使用时，必须首先加载`babel-register`
```js
require('babel-register');
require('./index.js')
```
如上，就不需要手动对`index.js`转码了

**注意**：`babel-register`只会对`require`命令加载的文件转码，而不会对**当前文件**转码。另外，由于它是**实时转码**，所以只适合在**开发环境**中使用。

## babel-core
如果某些代码需要 **调用Babel的API进行转码**，就要使用到`babel-core`模块
安装命令：`npm i -S babel-core`
然后，在项目中就可以调用`babel-core`
```js
var babel = require('babel-core');
// 字符串转码
babel.transform('code()', options);
// 文件转码(异步)
babel.transformFile('filename.js', options, function(err, result) {
    result;
 })
```
代码中的配置对象`options`，可以参看[官方文档](http://babeljs.io/docs/usage/api/)

下面例子：
```js
var es6Code = 'let x = n => n + 1';
var es5Code = require('babel-core')
  .transform(es6Code, {
    presets: ['latest']
  })
  .code;
  ```
  上面代码中，`transform`方法的第一个参数是一个字符串，表示要转换的ES6代码，第二个参数是转换的配置对象

## babel-polyfill
Bable默认只转换**新的JS句法(syntax)**，而**不转换新的API**，比如 `Iterator`、`Genrator`、`Set`、`Maps`、
`Proxy`、`Reflect`、`Symbol`、`Promise`等全局对象，以及一些定义在全局对象上的方法（比如Object.assign）都不会转码。

例如，ES6在Array对象上新增了`Array.from`方法。Babel就不会转码这个方法。如果想让这个方法运行，必须使用`babel-polyfill`，
为当前环境提供一个垫片。

安装命令如下：
`npm i -S babel-polyfill`
然后，在脚本头部，加入如下一行代码。
```js
import 'babel-polyfill';
//或者
require('babel-polyfill');
```
Babel默认不转码的API 非常多，详细清单查看[definitions.js](https://github.com/babel/babel/blob/master/packages/babel-plugin-transform-runtime/src/definitions.js)

## 浏览器环境
Babel看也可以用于浏览器环境，用的模块是：`babelife`模块
PS: 这部分内容不是很明白

## Babel与其他工具的配置
许多工具需要Babel进行前置转码，如：ESLint和Mocha，那么在使用这些工具时，需要先使用Babel转码

## Traceur转码器
Google公司的[Traceur](https://github.com/google/traceur-compiler)转码器，也可以将ES6代码转为ES5代码

