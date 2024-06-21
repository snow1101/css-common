# css 好文
* [CSS的N个编码技巧](https://juejin.cn/post/6924206099193135111) (1. 九宫格图片展示 2.background-origin：content-box 3.蚂蚁行军边框 4.clip-path 5.伪类扩大可点击区域 6.毛玻璃效果 7.css fliter 8.动画属性 水波纹等)
* [解剖postCSS](https://mp.weixin.qq.com/s/RuSWiouxkVI87bbC-4sEtw)

# css-common
常用的css总结

### 伸缩盒子的超出一行文本溢出方案

```
<style>
.wrap {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}
.wrap child{
  flex: 1;
   width: 0;
}
.ellipsis {
    overflow:hidden;
    text-overflow:ellipsis;
    white-space:nowrap;
}
.btn {
    width: 80px;
    height:25px;
}
</style>
<div class='wrap'>
    <div class='child'>
    	<h3 class="ellipsis">testtesttesttesttesttesttest</h3>
    </div>
    <div class='btn'>提交</div>
</div>
```

### CSS 整块文本溢出省略方案
![warp](./img/wrap.png)


```javascript
<style>
.wrap {
   width: 200px;
    white-space: normal;
    overflow : hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 1;
    -webkit-box-orient: vertical;
}
.wrap span{
  display: inline-block;
  padding: 5px 10px;
  background-color: purple;
  border-radius: 5px; 
}
</style>
<div class='wrap'>
  <span>aaaaaaa</span>
  <span>bbbbbb</span>
  <span>vvvvvv</span>
  <span>hhhhhhh</span>
</div>
```

### 长度单位又可以分为相对长度单位和绝对长度单位

(1) 相对长度单位。相对长度单位又分为相对字体长度单位和相对视区长度单位。

* 相对字体长度单位，如 em 和 ex，还有 CSS3 新世界的 rem 和 ch(字符 0 的宽度)。
* 相对视区长度单位，如 vh、vw、vmin 和 vmax。

(2)绝对长度单位:最常见的就是 px，还有 pt、cm、mm、pc 等了解一下就可以，在我
看来，它们实用性近乎零，至少我这么多年一次都没用过。

### 选择器

* 伪类选择器:一般指前面有个英文冒号(:)的选择器，如:first-child 或:last-child 等。
* 伪元素选择器:就是有连续两个冒号的选择器，如::first-line::first-letter、::before 和::after。
* 后代选择器:选择所有合乎规则的后代元素。空格连接。
* 相邻后代选择器:仅仅选择合乎规则的儿子元素，孙子、重孙元素忽略，因此又称“子选择器”。>连接。适用于 IE7 以上版本。
* 兄弟选择器:选择当前元素后面的所有合乎规则的兄弟元素。~连接。适用于 IE7 以上版本。
* 相邻兄弟选择器:仅仅选择当前元素相邻的那个合乎规则的兄弟元素。+连接。适用于IE7 以上版本。

###。:first-child 和:first-of-type 的区别
```
<style>
// 在p不是其父元素的第一个字元素的时候。p:first-child 是不会生效的, 但是:first-of-type 会生效，因为选中的是一个p类型
p:first-child { color: red};
p:first-of-type { color: blue};
</style>
<div>
	<div>aaaaa</div>
	<p>tjagjgeja</p>
	<p>tjagjgeja</p>
	<p>tjagjgeja</p>
	<p>tjagjgeja</p>
<div>
```

### “块级元素”和“display 为 block 的元素”不是一个概念

   例如li元素默认的 display 值是 list-item，table元素默认的 display 值是 table，但是它们 均是“块级元素”，因为它们都符合块级元素的基本特征，也就是一个水平流上只能单独显示一 个元素，多个块级元素则换行显示。
   
### 在设置reset.css的时候可以加上

```css
 input, textarea, img, video, object {
      box-sizing: border-box;
}
```

### 在公众号的热门文章中，经常会有图片，这些图片都是用户上传产生的，因此尺寸会有大有小，为了避免图片在移动端展示过大影响体验，常常会有下面的 max-width 限制:

```css
img {
      max-width: 100%;
      height: auto!important;
}
```
height:auto 是必需的，否则，如果原始图片有设定 height，max-width 生效的时候， 图片就会被水平压缩。强制 height 为 auto 可以确保宽度不超出的同时使图片保持原来的比 例。但这样也会有体验上的问题，那就是在加载时图片占据高度会从 0 变成计算高度，图文会 有明显的瀑布式下落。

### max-width 会覆盖 width
```css
<img src="1.jpg" style="width:480px!important;">
img { max-width: 256px; }
```
图片最后呈现的宽度是256px,style、!important 通通靠边站!因为 max-width 会覆盖 width。

### 所有的替换元素都是内联水平元素，但是，替换元素默认的 display 值却是不一样的

### 图片大小 
```css
img { width: 200px; height: 150px; }
<img src="1.jpg" width="128" height="96">
```
图片的固有尺寸为256 × 192
此时固有尺寸、HTML 尺寸和 CSS 尺寸同时存在，起作用的是 CSS 属性限定的尺寸， 因此，最终图片所呈现的宽高就是 200 像素×150 像素。

```css
img { width: 200px; }
<img src="1.jpg">
```
如果“固有尺寸”含有固有的宽高比例，同时仅设置了宽度或仅设置了高度，则元素依 然按照固有的宽高比例显示。所以，最终图片所呈现的宽高就是 200 像素×150 像 素(150 = 200 ×192 / 256)。
### css里的绝对居中

```
  .absolute-center{
    margin: auto;
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
  }
```

### 自适应屏幕，为了更好地用户体验，可以将最外层的div 设置

```
#container{
  max-width: 900px;
  margin: 0 auto;
}
```
### 倒三角图标

```
&:after{
  content: '';
  display: block;
  position: absolute;
  width: 0;
  height: 0;
  transform: translateX(-50%);
  bottom: 0;
  left: 50%;
  // background-color: #ff7e00;
  z-index: 1;
  border-bottom: 10px solid #ff7e00;
  border-top: 10px solid rgba(255, 255, 255, 0);
  border-left: 10px solid rgba(255, 255, 255, 0);
  border-right: 10px solid rgba(255, 255, 255, 0);
}

```

### 单行文本溢出，和多行文本溢出显示省略号

```
.singleText {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.multiText {
  display: -webkit-box;
	-webkit-box-orient: vertical;
	word-break: break-all;
	overflow: hidden;
  -webkit-line-clamp: 2;
}

```

### 使用flex布局以后，子元素的float, clear , 和vertical-align属性将失效

[flex布局参考](https://juejin.im/post/599970f4518825243a78b9d5)


### 美化选中的文本

```
<p>Custom text selection color</p>
::selection {
    color: red;
    background-color: yellow;
}
```

### CSS3中的伪类
* :root 选择文档的根元素，等同于 html 元素
* :empty 选择没有子元素的元素
* :target 选取当前活动的目标元素
* :not(selector) 选择除 selector 元素意外的元素
* :enabled 选择可用的表单元素
* :disabled 选择禁用的表单元素
* :checked 选择被选中的表单元素
* :nth-child(n) 匹配父元素下指定子元素，在所有子元素中排序第n
* :nth-last-child(n) 匹配父元素下指定子元素，在所有子元素中排序第n，从后向前数
* :nth-child(odd) 、 :nth-child(even) 、 :nth-child(3n+1)
:first-child 、 :last-child 、 :only-child
:nth-of-type(n) 匹配父元素下指定子元素，在同类子元素中排序第n
* :nth-last-of-type(n) 匹配父元素下指定子元素，在同类子元素中排序第n，从后向前数
* :nth-of-type(odd) 、 :nth-of-type(even) 、 :nth-of-type(3n+1)
* :first-of-type 、 :last-of-type 、 :only-of-type

### CSS3中的伪元素
* ::after 已选中元素的最后一个子元素
* ::before 已选中元素的第一个子元素
* ::first-letter 选中某个款级元素的第一行的第一个字母
* ::first-line 匹配某个块级元素的第一行
* ::selection 匹配用户划词时的高亮部分

### 对requestAnimationFrame的详细理解
requestAnimationFrame是一个Web API，用于优化动画效果并避免浏览器过度使用CPU资源。它允许您在下一次浏览器渲染之前安排一个回调函数。属于宏任务

使用requestAnimationFrame的好处是，它会在浏览器下一次绘制屏幕之前执行回调函数，因此可以确保回调函数在浏览器绘制下一帧之前完成。这可以防止闪烁、卡顿和其他不良动画效果，因为在下一帧绘制之前，回调函数的所有计算和更新都完成了。

使用requestAnimationFrame的基本步骤如下：

1.编写一个回调函数，该函数执行动画所需的任何计算和更新。

2.调用requestAnimationFrame函数，将回调函数作为参数传递。

3.在回调函数中，使用requestAnimationFrame再次调用自己，以便在下一帧之前继续更新和绘制动画。

```javascript
function animate() {
  // 计算和更新动画状态
  requestAnimationFrame(animate);
}

// 开始动画
requestAnimationFrame(animate);

```
请注意，使用requestAnimationFrame的代码可以在浏览器切换到后台时自动停止，这是因为浏览器会停止调用requestAnimationFrame，以便节省CPU资源。
**优势**：
* **cpu节能：** 使用SetTinterval 实现的动画，当页面被隐藏或最小化时，SetTinterval 仍然在后台执行动画任务，由于此时页面处于不可见或不可用状态，刷新动画是没有意义的，完全是浪费CPU资源。而RequestAnimationFrame则完全不同，当页面处理未激活的状态下，该页面的屏幕刷新任务也会被系统暂停，因此跟着系统走的RequestAnimationFrame也会停止渲染，当页面被激活时，动画就从上次停留的地方继续执行，有效节省了CPU开销。
* **函数节流：** 在高频率事件( resize, scroll 等)中，为了防止在一个刷新间隔内发生多次函数执行，RequestAnimationFrame可保证每个刷新间隔内，函数只被执行一次，这样既能保证流畅性，也能更好的节省函数执行的开销，一个刷新间隔内函数执行多次时没有意义的，因为多数显示器每16.7ms刷新一次，多次绘制并不会在屏幕上体现出来。
* **减少dom操作：** requestAnimationFrame 会把每一帧中的所有DOM操作集中起来，在一次重绘或回流中就完成，并且重绘或回流的时间间隔紧紧跟随浏览器的刷新频率，一般来说，这个频率为每秒60帧。

### setTimeout执行动画的缺点

* 不够流畅：setTimeout会在固定的时间间隔后执行回调函数，这意味着动画的更新速度不是固定的。这可能导致动画在某些时间间隔内显得不够流畅。

* 时间不准确：由于setTimeout的执行时间依赖于当前系统的工作负载和其他因素，因此它的执行时间不够准确。这可能导致动画不够流畅或出现卡顿。

* 对CPU的压力较大：由于setTimeout在固定时间间隔后执行回调函数，因此浏览器需要持续不断地检查是否已经达到了指定的时间间隔。这会对CPU造成一定的压力，特别是在执行大量动画时。

* 不同设备表现差异：不同的设备具有不同的CPU性能和其他硬件差异，因此使用固定的setTimeout时间间隔会导致不同设备上的动画效果有所不同。

因此，使用requestAnimationFrame来执行动画通常是更好的选择。它会优化动画效果并避免浏览器过度使用CPU资源，可以确保动画在下一帧绘制之前完成，从而产生更流畅、更准确和更一致的动画效果。

### 为什么有时候⽤translate来改变位置⽽不是定位？ 
使用 translate 来改变元素的位置比使用定位（position）有以下优点：
1. 性能更好：使用 translate 不会触发浏览器对元素重新布局（reflow）或重绘（repaint），这可以减少浏览器的工作量，从而提高网页的性能和响应速度。相比之下，改变元素的定位需要浏览器重新计算元素的位置和布局，这会更加昂贵。

2. 更加精确：使用 translate 可以非常精确地控制元素的位置，因为它使用的是相对于元素自身的坐标系，而不是相对于父元素或文档的坐标系。这意味着可以轻松地实现元素的微调和动画效果。

3. 更加灵活：使用 translate 可以更加灵活地改变元素的位置，因为可以通过 JavaScript 动态地修改 transform 属性来实现不同的动画效果。而使用定位则需要提前计算好元素的位置和大小，并且无法动态调整。

需要注意的是，使用 translate 改变元素的位置不会影响文档流（document flow），也就是说，其他元素的位置和大小不会受到影响。这意味着使用 translate 可以更加灵活地布局和排版网页，但也需要注意元素的层叠顺序（z-index）以避免遮挡问题。

### 替换元素的概念及计算规则
替换元素（replaced element）是指在渲染过程中，浏览器根据元素的标签和属性值，从外部资源（如图像、视频、音频等）中获取内容来渲染的元素。替换元素的内容不直接包含在HTML文档中，而是从外部资源中加载。常见的替换元素包括<img>、<video>、<audio>、<iframe>、<canvas>等。

替换元素的尺寸大小计算规则如下：

1. 如果替换元素有明确的指定宽度和高度（使用CSS属性width和height），则使用这些值作为元素的尺寸大小。

2. 如果没有指定宽度和高度，但是在HTML标签中指定了元素的宽度和高度（如 img src="example.png" width="200" height="100"），则使用这些值作为元素的尺寸大小。

3.如果没有指定宽度和高度，并且HTML标签中也没有指定，但是替换元素本身具有固定的默认宽度和高度（如<img>元素的默认宽度和高度），则使用这些默认值作为元素的尺寸大小。

4. 如果没有指定宽度和高度，并且HTML标签中也没有指定，替换元素也没有固定的默认宽度和高度，则将元素的尺寸大小设为0。

需要注意的是，替换元素的尺寸大小是根据内容本身的大小来计算的，而不是根据CSS盒模型来计算的。因此，替换元素的盒模型属性（如padding、border和margin）不会影响它们的尺寸大小。

### 什么是物理像素，逻辑像素和像素密度？
物理像素（physical pixel）是指显示器或手机屏幕上的最小物理显示单元。它是由硬件决定的，通常是一个红、绿、蓝三个亮点（即RGB颜色），组合成一个物理像素点。

逻辑像素（logical pixel）也称为设备独立像素（device-independent pixel），是指在开发者看来的屏幕上的最小显示单元。它是为了让开发者能够以相对一致的方式开发移动应用程序，无论是在高密度屏幕还是低密度屏幕上，都能够实现一致的显示效果。

像素密度（pixel density）是指在屏幕或显示设备上每英寸显示的像素数。它通常以PPI（pixels per inch）作为单位，表示每英寸内显示的像素数量。像素密度越高，显示效果就越细腻，细节也越清晰。

在高密度屏幕中，一个逻辑像素可能对应着多个物理像素，这样可以让同样大小的元素在高密度和低密度屏幕上看起来大小一致，同时也能够让文字和图像在高密度屏幕上保持清晰。而在低密度屏幕上，一个逻辑像素只对应一个物理像素。

在Web开发中，为了适配不同的设备屏幕，需要使用适当的像素密度、逻辑像素和物理像素的概念，同时需要使用响应式设计和流式布局等技术，以确保在不同的屏幕上都能够实现一致的显示效果。
可以使用 CSS 媒体查询来判断不同的像素密度，从而选择不同的图片
