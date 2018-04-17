# css-common
常用的css总结


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
