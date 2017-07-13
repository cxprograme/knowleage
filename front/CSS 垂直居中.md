# CSS 垂直居中

一般情况下，我们大家都知道对于元素如何实现水平居中:

* 对于inline元素：通过text-align:center
* 对于block元素：通过margin: 0 auto

## 实现元素垂直居中

这里介绍六种垂直居中的方法。

### vertical-align

vertiacal-align:middle 但其只适用于table-cell 中的内容

````css
<div class="parent">
  <div class="child">Content here</div>
</div>
.parent {display: table;}
.child {
  display: table-cell;
  vertical-align: middle;
}
````

### line-height

适用于设置单行文本和图片的垂直居中，只需将line-height属性设置大于font-size，且等于容器的高度。

````css
<div class="content">
  Text here
</div>
.content{
  height:200px; /*不必要*/
  line-height: 200px;
}
````

当然，我们也可以不设置父级元素的高度，而是让子元素将其撑开，同样能达到效果。同理，图片和单行文本一样，也为`inline`元素，也可以通过设置容器的`line-height`达到居中效果：

````css
<div class="content">
  <img src="image.png" alt="" />
</div>
.content {
  line-height: 200px;
}
#parent img {
  vertical-align: middle; /*调整基线位置，不是设定垂直居中哦~*/
}
````

### 绝对定位+margin

````css
<div class="parent">
  <div class="child">Content here</div>
</div>
.parent {
  position: relative;
  height: 800px;
}
.child {
  position: absolute;
  top: 50%;
  left: 50%;
  height: 30%;
  width: 50%;
  margin: -15% 0 0 -25%; /*margin 为负值且为自身尺寸的一半*/
}
````

这种方法会出现父级元素内容溢出，所以最好在知道父级元素的高度和宽度的情况下使用。

### 绝对定位+ Stretching

通过绝对定位设置top，bottom，right，left 值为0，将目标元素拉伸至父元素 的四个边，在设置margin为auto，使得上下左右相等，完全实现居中效果，适用于所有的block元素。

````css
<div class="parent">
  <div class="child">Content here</div>
</div>
.parent {
  position: relative;
  height: 300px;
}
.child {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  width: 50%;
  height: 30%;
  margin: auto;
}
````

这种方法在IE8不适用。

### 绝对定位+ transform3d

这里通过绝对定位将目标元素左上角定位在父级元素的中央位置，然后通过设定目标元素的`transform3d`属性使其中心点与父级元素重合，适用于所有`block`元素。

````css
<div class="parent">
  <div class="child">Content here</div>
</div>
.parent {
  position: relative;
  height: 300px;
}    
.child {
  position: absolute;
  top:50%;
  left:50%;
  width: 150px;
  height: 130px;
  transform:translate3d(-50%,-50%,0); /*向左向上移动自身尺寸的一半*/
}
````

### CSS3 Flex

````css
<div class="parent">
  <div class="child">Content here</div>
</div>
.parent {
  display: flex;
  display: -webkit-box;
  display: -webkit-flex;

  display: -moz-box;
  display: -moz-flex;
  display: -ms-flexbox;

    /* 子元素主轴（默认为水平轴）上居中*/
  -webkit-box-align: center;
  -moz-box-align: center;
  -ms-flex-pack:center;/* IE 10 */
  -webkit-justify-content: center;
  -moz-justify-content: center;
  justify-content: center;/* IE 11+,Firefox 22+,Chrome 29+,Opera 12.1*/

  /* 子元素交叉轴（默认为纵轴）居中 */
  -webkit-box-pack: center;
  -moz-box-pack: center;
  -ms-flex-align: center;/* IE 10 */

  -webkit-align-items: center;
  -moz-align-items: center;
  align-items: center;

  height: 300px;
}

.child {
  width: 150px;
  height: 130px;
}
````

