### 前端性能优化方案
#### 1.减少请求数量
##### 文件（可通过webpack以及相关插件进行优化）
- 公共库合并
- 不同页面单独合并
- 提取公共代码
##### 图片
- 雪碧图、精灵图（不推荐，不好维护）
- base64、svg(代码形式，嵌套在html里)
- icon
##### 减少重定向
尽量避免使用重定向，当页面发生了重定向，就会延迟整个html文档的传输。在HTML文档到达之前，页面中不会呈现任何东西，也没有任务组件会被下载，降低了用户体验

如果一定要使用重定向，如http重定向到https，要使用301永久重定向，而不是302临时重定向。因为，如果使用302，则每一次访问http，都会被重定向到https的页面。而永久重定向，在第一次从http重定向到https之后，每次访问http，会直接返回https的页面

##### 使用缓存
- 强缓存和协商缓存（expires,cache-control,last-modified,etag）
- css不使用@import(@import会造成额外的请求)
- 避免空src和href(a标签的herf会造成重定向)

#### 2.减少资源大小
##### 压缩资源（通过webpack）
- html压缩、css压缩、js压缩、图片压缩（可使用在线压缩）
- 服务器开启gzip
这一般是指WWW服务器中安装的一个功能，当有人来访这个服务器的网站时，服务器中的这个功能就将网页内容压缩后传输来访的电脑浏览器中显示出来。一般对纯文本内容可以压缩原大小的40%

#### 3.优化网络传输
- 使用cdn
- dns预解析（DNS Prefetch）
- 并行连接
- 持久性连接
- 管道话连接

#### 4.优化资源加载
- 资源加载位置（css放head中，js放body底部）
- 异步script(async，defer)
- 模块按需加载
- 资源懒加载与资源预加载

#### 5.减少回流重绘
- css选择器优化（避免使用层级较深的选择器，或其他一些复杂的选择器）
- 避免使用css表达式（expression）
- 动态加载内容的元素设置高度或最小高度（元素加载内容可以造成回流）
- 不要使用tabel布局（一个小的改动有可能造成整个tabel重新布局，tabel渲染通常3倍于同等元素时间）
- 能使用css实现的效果，尽量使用css不使用js实现
- 需要多次渲染的元素，可以设置absolute,可以减少重绘范围
- 减少Dom的深度以及DOM数量
- 事件委托（可以减少内存使用，提高性能及降低代码复杂度）
- 防抖和节流（限制某个方法的频繁触发）

#### 6.使用更好的AIP
- 样式选择器
- requestAnimationFrame代替setTimeout和setIerval
#### 7.webpack优化
- 打包功能代码
- 动态导入和按需加载
- 剔除无用的代码
- 长缓存优化（将hash替换chunkhash）