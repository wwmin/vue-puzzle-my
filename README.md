在命令行中安装webpack：

$ npm install -g webpack
安装本地库（作为dev dependencies），需要在package.json中添加devDependencies的部分。

"babel-core": "^6.1.2",
"babel-loader": "^6.1.0",
"babel-plugin-transform-runtime": "^6.1.2",
"babel-preset-es2015": "^6.1.2",
"babel-preset-stage-0": "^6.1.2",
"babel-runtime": "^5.8.0",
"webpack": "^1.12.2"
在保存后，运行：

$ npm install

注意我推荐用的是Vue初学者工具中最佳支持的版本，因为有时候最新的版本不能很好的支持。

最后，vuejs库安装到你的dependencies中。

$ npm install --save vue
如今你可以创建一个app用WebPack，运行

$ webpack


$ npm install
$ npm install -g webpack-dev-server
$ webpack-dev-server --inline --hot