#pomelo-loader
pomelo中使用Convention over Configuration的形式管理工程目录，不同的功能按约定放在不同的目录下。pomelo-loader为pomelo提供了按目录加载模块的功能。
pomelo-rpc可以批量加载指定目录下的模块，挂到一个空对象下返回（但不会递归加载子目录），同时提供模块命名和替换机制。
模块命名
模块默认以文件名为名。如：加载lib/a.js后，返回的结果为：{a: require('./lib/a')}。
如果模块中定义了name属性，则会以name作为模块的名称。如：
a.js
exports.name = 'test';
返回的结果为：{test: require('./lib/a')}


##安装
```
npm install pomelo-loader
```

##用法
``` javascript
var Loader = require('pomelo-loader');

var res = Loader.load('.');
console.log('res: %j', res);
``` 

##API
###Loader.load(path, context)
加载path目录下所有模块。如果模本身是一个function，则把这个function作为获取模块的工厂方法，通过调用这个方法获取到模块实例;否则直接返回加载到的模块。
####参数
+ path 加载的目录
+ context 如果通过工厂方法加载模块，会将该参数作为初始化参数传给工厂方法。
