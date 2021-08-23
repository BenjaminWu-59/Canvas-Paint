# Canvas 实践—画图板

### 画线处理

#### 第一步：画点原理

关键属性：`clientX`,`clientY`

通过点击事件，可以拿到属性: `clientX`,`clientY`，他们可以获取点击页面时的坐标。 

假设：当每次点击时，我们都会创建一个名为canvas的div，这个div的位置就是我们点击时的位置：

```js
canvas.style.top = 点击.clientY + 'px'
canvas.style.left = 点击.clientX + 'px'
```

接着加边框和宽高度，就可以实现每次点击都会出现一个点了。

后面优化可以使用鼠标事件来润色！



#### 第二步：画线原理

关键属性：ctx

MDN文档中的教程有这么一段代码：

```js
function draw() {
  var canvas = document.getElementById('canvas');
  if (canvas.getContext) {
    var ctx = canvas.getContext('2d');

    ctx.beginPath();
    ctx.moveTo(75, 50);
    ctx.lineTo(100, 75);
    ctx.lineTo(100, 25);
    ctx.fill();
  }
}
```

这是一个三角形。三角形的线是如何形成的？

经过测试，发现画线的关键代码是：

```js
ctx.moveTo();//开始的点
ctx.lineTo();//结束的点
ctx.stroke();//保证线出现
```

得知画线的真相，我们可以直接做一个画线的函数：

```js
function drawLine(x1, y1, x2, y2) {
          ctx.beginPath();
          ctx.moveTo(x1, y1);
          ctx.lineTo(x2, y2);
          ctx.stroke();
        }
```

后面将其和画点结合，就可以实现画线功能了。（无数点组成线）

这里需要注意的是，我们的点在移动的时候，每一次的起点都应该是上一个点，这样才能保证我们能画出去曲线。这个需要你自己去看代码了。



### 擦除功能（研究中...）
