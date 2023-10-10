# htmlWebpackPlugin 插件的使用

## 作用
> 根据webpack的输出，自动将输出文件添加到模板html中，生成新的html。

## 安装
    npm i html-webpack-plugin -D

## 参数

### title 设置html的标题
    // html
    <title> <%= htmlWebpackPlugin.options.title %> </title>

### filename 设置生成的html的文件名字

### template 设置html模板路径
> 默认是当前webpack配置文件下面的index.ejs文件

### templateContent 设置模板字符串
> 值的类型可以是：string | function | boolean
    new HtmlWebpackPlugin({
        templateContent: ({htmlWebpackPlugin}) => {
            return <html>
                <head>
                    <title>
                        ${htmlWebpackPlugin.options.title}
                    </title>
                </head>
            </html>
        }
    })
 
### templateParameters 设置模板参数
>值的类型：boolean | object | function
    // webpack.config.js
    new HtmlWebpackPlugin({
        templateParameters: {
            foo: 'bar'
        }
    });

    // html
    <div> <%= foo %> </div>

    // 编译完成之后生成的html文件
    <div>bar</div>

### inject 
> 值可以是：true（默认）、false、'body'、'head'
    body: 代表自动注入的js是注入到body的最后
    head：代表自动注入的js是注入到head的最后
    false：代表关闭自动注入
    true：代表自动注入的js是注入到body的最后还是head的最后取决于配置项scriptLoading 

### scriptLoading
> 值可以是：'blocking' | 'module' | 'defer'
    blocking：配合inject=true，将js插入到body的最后
    module：配合inject=true，将js插入到head的最后，同时给script标签添加属性type=module（使用模块化，可以在这个script标签体内使用import和export）
    defer：配合inject=true，将js插入到head的最后，同时给script标签添加属性defer （代表异步加载该标签体内容）

### publicPath
> string | 'auto'
    会在生成的js引入到html中的时候加上这个参数的值，重新构成新的路径

### favicon
> string
    html的图标路径

### meta 加到html的head中meta标签中
> object
    {viewport: 'width=device-width, initial-scale=1, shrink-to-fit=no'}

### base
> object | string | false   比如由base制定了一个URL地址，接下来你所要调用的文件或图片等就无须再填写完整的地址，只需写上该文件名或图片名即可，比如由base制定了一个URL地址，接下来你所要调用的文件或图片等就无须再填写完整的地址，只需写上该文件名或图片名即可
    插入一个base标签

### minify 是否压缩html
> boolean | object 默认production环境下为true，开启压缩

### hash 是否在生成的js和css文件的链接上面加上hash
> boolean 默认是false

### cache 是否启用缓存
> boolean 默认是true

### showErrors
> boolean 默认是true 如果 webpack 编译出现错误，webpack会将错误信息包裹在一个 pre 标签内

### chunks 引入指定的chunks
> array 对应entry中的名字

### chunksSortMode chunks引入的js的排序
> 'none', 'auto', 'manual' | function  auto是根据entry中写入的顺序进行引入，manual是根据chunks中写入的顺序去引入

### excludeChunks 允许你跳过某些chunks，使其不必引入
> array

### xhtml 如果为true，则将链接标记呈现为自关闭（符合XHTML）像meta title标签
> boolean 默认为false


## webpack.config.js中的使用
    const HtmlWebpackPlugin = require('html-webpack-plugin');

    module.exports = {
        plugins: [
            new HtmlWebpackPlugin({
                title: '',
                ...
            })
        ]
    }