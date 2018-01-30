

##小记
### Webpack

* `file-loader`

`file-loader`可以把 JavaScript 和 CSS 中**导入图片的语句替换成正确的地址**，并同时把文件输出到对应的位置。

比如源css
```css
#app {
  background-image: url(./imgs/test.png);
}
```
经过`file-loader`转换后

```css
#app {
  background-image: url(5556e1251a78c5afda9ee7dd06ad109b.png);
}
```

并且在输出目录 dist 中也多出 ./imgs/test.png 对应的图片文件 7566e1251a78c5afda9ec7dd06ac109b.png,**输出的文件名是根据文件内容的计算出的 Hash值**

* `url-loader`

url-loader 可以把**文件的内容经过 base64 编码后注入到 JavaScript 或者 CSS 中去**

一般利用 `url-loader` 把网页需要用到的**小图片资源**注入到代码中去，以减少加载次数。

考虑到这样做有可能会使JS或者CSS文件增大，所以提供了一个方便的选择 **limit**，该选项用于控制当文件大小小于 limit 时才使用 `url-loader`，否则使用 **fallback** 选项中配置的 loader。Webpack 配置例子：

```js

module.exports = {
  module: {
    rules: [
      {
        test: /\.png$/,
        use: [{
          loader: 'url-loader',
          options: {
            // 30KB 以下的文件采用 url-loader
            limit: 1024 * 30,
            // 否则采用 file-loader，默认值就是 file-loader 
            fallback: 'file-loader',
          }
        }]
      }
    ]
  },
};
```

### 模块

* `chokidar` 提供更好的监听文件方法