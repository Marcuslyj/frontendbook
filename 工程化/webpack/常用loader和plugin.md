#### loader数组的执行从右到左



### css-loader

加载css文件，并转换commonjs对象

#### style-loader

将样式通过style标签插入到head中

#### file-loader

处理文件（图片字体等）

#### url-loader

功能类似file-loader，基于file-loader

可以做base64 转换

#### postcss-loader

autoprefixer

#### px2rem-loader

+手淘lib-flexible库

#### raw-loader

内联html、js等

```ejs
<sctipt>$require('raw-loader!babel-loader!./meta.html')</sctipt>
```

```ejs
<sctipt>$require('raw-loader!babel-loader!../node_modules/lib-flexible')</sctipt>
```





#### MiniCssExtractPlugin

分离css

#### clean-webpack-plugin

自动清理构建目录

















