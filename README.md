# 这是一个vue 的小项目

## [主流开源协议之间有何异同？](https://www.zhihu.com/question/19568896)

## 用(传统方式)命令行把修改过后的代码上传到码云？？？
1. git add .
2. git commit -m "提交信息"
3. git push

## 制作首页  App 组件
1. 完成 Header 区域，使用的是 Mint-UI 中的Header 组件
2. 制作底部的 Tabbar 区域，使用的是 MUI 的 Tabber.html
 + 在制作 购物车 小图标的时候，操作相对多一点；
 + 把 扩展图标 的css样式， 扩展字体库 ttf 文件，拷贝到项目中；
 + 为 购物车 小图标， 添加样式 ‘mui-icon mui-icon-extra mui-icon-extra-cart’ 
3. 要在 中间区域 放置一个 router-view 来展示路由匹配到的组件

## 改造 tabber 为 router-link

## 设置路由高亮

## 点击 tabber 中的路由链接，展示对应的路由组件

## 制作首页轮播图布局

## 加载首页轮播图数据
 1.  获取数据， 使用 vue-resource 获取数据
 2.  使用 vue-resource 的 this.$http.get 获取数据
 3.  获取到的数据，要保存到 data 身上
 4.  使用 v-for 循环渲染 每个 item 项

## 通过改造 MUI 中九宫格的样式，来实现六宫格效果 

## 设置路由重定向

## 改造 新闻资讯 路由链接

## 新闻资讯 页面制作
1. 绘制界面， 使用MUI 中的 media-list.html
2. 使用 vue-resource 获取数据
3. 渲染 真实数据

## 实现 新闻资讯列表 点击跳转到新闻详情
1. 把列表中的每一项改造为 router-link ，同时， 在跳转的时候应该提供唯一的 ID 标识符
2. 创建新闻详情的组件页面 NewsList.vue
3. 在 路由模块中， 将新闻详情的 路由地址 和 组件页面 对应起来

## 实现新闻详情的页面布局 和 数据渲染

## 单独封装一个 comment.vue 评论子组件
1. 先创建一个 单独的 comment.vue 组件模板
2. 在需要使用 comment 组件的页面中，先手动导入 comment 组件
    + 'import comment from './comment.vue''
3. 在父组件中， 使用 'components' 属性， 将刚才导入 comment 组件，注册为自己的子组件
4. 将注册子组件的时候，注册名称，以 标签形式， 在页面中引入即可

## 获取所有的评论数据显示到页面中
    1. getcomments 

## 实现点击加载更多评论的功能 
1. 为加载更多按钮，绑定点击事件，在事件中，请求 下一页数据
2. 点击加载更多， 让pageIndex++, 然后重新调用 this.getComments() 方法重新获取最新一页的数据
3. 为了防止 新数据 覆盖 老数据的情况， 我们在点击加载更多的时候，每当获取到新数据，应该让老数据调用 数组的 concat方法，拼接上新数组

## 发表评论
1. 把文本框做双向数据绑定
2. 为发表按钮绑定一个事件
3. 校验评论内容是否为空，如果为空，则 Toast 提示用户 内容不能为空
4. 通过 vue-resouce 发送一个请求，把评论内容提交给服务器
5. 当评论发表 OK 后，重新出啊新列表，以查看最新的评论
    + 如果调用 getcomments 方法重新刷新评论列表的话， 可能只能得到最后一页的评论，前几页的评论获取不到
    + 换种思路： 当评论成功后，在客户端，手动拼接一个 最新的评论对象，然后调用数组的 unshift 方法，把最新的评论，追加到 data 中 comments 开头， 这样就能完美实现刷新评论列表的需求


## 改造 图片分析按钮为路由的链接并显示对应的组件页面

## 绘制 图片列表 组件页面结构并美化样式
1. 制作 顶部的滑动条
2. 制作 底部的图片列表

###  制作 顶部滑动条 的坑们 ：
 1. 借助于 MUI中的 tab-top-webview-main.html
 2. 需要把 slider 区域的 mui-fullscreen 类去掉
 3. 滑动条无法正常触发滑动，通过检验官方文档，发现这是js组件，需要被初始化一下：
    + 导入mui.js
    + 调用官方提供的 方法 去初始化：
    、、、
        mui('.mui-scroll-wrapper').scroll({
	        deceleration: 0.0005 //flick 减速系数，系数越大，滚动速度越慢，滚动距离越小，默认值0.0006
        });
    、、、
4. 在初始化 滑动条的时候，导入的mui.js ,但是，控制台报错：'Uncaught TypeError: 'caller', 'callee', and 'arguments' properties may not be accessed on strict mode functions or the arguments objects for calls to them' 
    + 合理推测，觉得可能是mui.js 中用到了'caller', 'callee', and 'arguments' 东西，但是，webpack打包好的 bundle.js中，默认是启用严格模式的，所以这两者冲突了
    + 解决方案： 1. 把mui.js中非严格模式的代码改掉；但是不现实；
        2. 把webpack 打包时候的严格模式禁用掉；
    + 最终选择了 第二种  移除严格模式： 使用这个插件babel-plugin-transform-remove-strict-mode
5. 刚进入图片页面分享的时候，滑动条无法正常工作，，如果要初始化 滑动条，必须要等DOM元素加载完毕，所以，把 滑动条的代码，放到mounted 生命周期函数中
6. 当滑动条 调试OK后，tabbar 无法正常工作，，，需要把 每个tabbar 按钮的样式中 ‘mui-tab-item ’ 重新改名字
7. 获取所有分类，并渲染分类列表

###  制作图片列表区域
1. 图片列表需要使用懒加载技术，可以使用mint-UI 提供的组件 'lazy-load'
2. 根据 'lazy-load' 的使用文档， 使用
3. 渲染图片列表数据

### 实现了图片列表的懒加载改造 和 样式美化

## 实现了点击图片 跳转到图片详情页面
1.  在改造 li 成 router-link 的时候，需要使用 tag 属性指定要渲染为哪种元素


##  实现 详情页面的布局和美化 ， 同时获取数据渲染页面

## 实现 图片详情中 缩略图的功能
1. 使用 插件 vue-preview 这个缩略图插件
2. 使用 vue-preview标签，引入样式
3. 注意： 每个图片数据对象中， 必须有 w 和 h ，msrc（更新后必须加）属性

## 手机上 进行项目的预览 和测试
1. 手机正常运行
2. 保证 手机 和开发项目的电脑 处于同一个局域网， 就是说： 手机可以访问到电脑的 Ip
3. 打开自己的 项目中 package.json 文件，在 Ddev 脚本中，添加一个 --host 指令，把当前电脑的局域网 IP地址，设置为 --host 的指令值
  + 在 cmd终端中 运行 "ipconfig"， 查看无线网的IP地址