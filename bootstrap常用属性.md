## container-fluid
将宽度设定为auto，所以当缩放浏览器时，它会保持全屏大小，始终保持100%的宽度
## img-responsive
图片适配屏幕宽度
## text-center
块元素居中显示
## btn
bootstrap button样式
### btn-block 
使button成为块级元素（按钮将会伸展并填满页面整个水平空间，任何在它之下的元素都会跟着浮动至该区块的下一行。）
### btn-primary
深蓝色主题
### btn-info 
浅蓝色主题，被用在那些用户可能会采取的操作上。
### btn-danger
红色主题，被用来提醒用户该操作具有“破坏性”。
## 响应式网格布局

响应式网格布局|超小设备手机（<768px）|小型设备平板电脑（≥768px）|中型设备台式电脑（≥992px）|大型设备台式电脑（≥1200px）
---|---|---|---|---
网格行为|一直是水平的|以折叠开始，断点以上是水平的|以折叠开始，断点以上是水平的|以折叠开始，断点以上是水平的
最大容器宽度|None (auto)|750px|970px|1170px
Class 前缀|.col-xs-|.col-sm-|.col-md-|.col-lg-
列数量和|12|12|12|12
最大列宽|Auto|60px|78px|95px
间隙宽度|30px（一个列的每边分别 15px）|30px（一个列的每边分别 15px）|30px（一个列的每边分别 15px）|30px（一个列的每边分别 15px）
可嵌套|Yes|Yes|Yes|Yes
偏移量|Yes|Yes|Yes|Yes
列排序|Yes|Yes|Yes|Yes
## Font Awesome 图标库
    <link rel="stylesheet" href="//cdn.bootcss.com/font-awesome/4.2.0/css/font-awesome.min.css"/>
    eg. <i class="fa fa-info-circle"></i>
为<i></i>标签加相应属性设置图标

### form-control
输入框样式
### well
创造视觉上的一种深度感
