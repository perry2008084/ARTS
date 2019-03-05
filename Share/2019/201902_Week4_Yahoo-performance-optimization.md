
## 性能优化

学习了一下雅虎有关网站性能优化的35条最佳实践

* 减少http请求
1. 合并文件
2. CSS雪碧图
3. 内联图片,base64编码

* 使用CDN
* 添加一个`Expires`或者`Cache-Control`header
* 压缩内容(Accept-Encoding: gzip, deflate)
* 将样式表放置在顶部(文档head)
* 将脚本放置在底部(defer)
* 避免使用CSS表达式(仅IE支持)
* 将JavaScript和CSS放在外部文件中
* 减少DNS查找
* 压缩JavaScript和CSS
* 避免重定向
* 移除重复的脚本
* 配置ETags(Entity tags，有利有弊)
* 让Ajax请求缓存
* Flush the Buffer Early
* 在AJAX请求中使用GET
* 延迟加载组件
* 预加载组件
* 减少DOM元素数量
* 分割组件到多个域名(并行加载)
* 减少iframe数量
* 不要404
* 减少cookie的大小
* 给组件使用无cookie的域名
* 减少DOM访问
* 开发更智能的事件处理器
* 使用<link>替换@import(import无法并行加载)
* 避免使用过滤(IE7以下)
* 优化图片(推荐png格式)
* 优化CSS雪碧图
* 不要在HTML中缩放图片
* 让favicon.ico更小和可缓存
* 保持组件的大小在25K以下
* 打包组件到多部件文档(Multipart document)
* 避免Image属性src为空

## CSS盒模型

1. Content,Padding,Border,Margin; 标准盒模型和IE盒模型
2. 区别: 宽度和高度的计算方式不同，标准只计算内容，IE包含padding和border
3. 设置: box-sizing: content-box; box-sizing: border-box;
4. CSS盒模型获取元素的宽度和高度:
```js
dom.style.width/height
dom.currentStyle.width/height
window.getComputedStyle(element).width/height
dom.getBoundingClientRect().width/height
```
