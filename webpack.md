## webpack

#####  1.介绍一下webpack基本的属性？

```
const path = require('path')
module.exports = {
    entry: { // main是默认入口，也可以是多入口
        main: './src/main.js'
    },
    // 出口
    output: {
        filename: './build.js', // 指定js路径
        path: path.join(__dirname, '..', '', 'dist') // 最好是绝对路径
        // 代表上一级的dist
    },
    module: {
        // 一样的功能rules: webpack2.xx新加的
        loaders: [ // require('./a.css||./a.js')
            {
                test: /\.css$/,
                loader: 'style-loader!css=loader',
                //多个loader用!分割
                //顺序是反过来的 2!1  多个loader
            },
            {
                test: /\.(jpg|svg)$/,
                loaderL 'url-loader?limit=4096&name=[name].[ext]',
                // limit=4096&name=[name].[ext]' 多个参数之间用&符号分割
                //[name].[ext]内置提供的
                options: {
                    limit: 4096,
                    name: '[name].[ext]'
                }
            }
        ]  
    },
    plugins: [
        // 插件的执行顺序是依次执行的，和loader是反过来的
        new htmlWebpackPlugin({
            template: './src/index.html',
        })
        // 将src下的template属性描述的文件根据当前配置的output.path，将文件移动到该目录。
        // 在插件的执行过程中，它本身可以去拿当前所设置的webpack选项，便于对webpack选项的复用，
    ]
}
```
##### 2.babel转换es6语法工作原理？
- babel是一个转译器，感觉相对于编译器compiler，叫转译器transpiler更准确，因为它只是把同种语言的高版本规则翻译成低版本规则，而不像编译器那样，输出的是另一种更低级的语言代码。
但是和编译器类似，babel的转译过程也分为三个阶段：parsing、transforming、generating，以ES6代码转译为ES5代码为例，babel转译的具体过程如下：

```
ES6代码输入 ==》 babylon进行解析 ==》 得到AST
==》 plugin用babel-traverse对AST树进行遍历转译 ==》 得到新的AST树
==》 用babel-generator通过AST树生成ES5代码
```