# vue中实现拖动调整左右两侧div的宽度

html部分：

```bash
<template>
	<div class="container">
		<div class="left">
			<div class="left-tree"></div>
            <div class="left-resize"></div>
            <div class="left-table"></div>
		</div>
		<div class="resize"></div>
		<div class="right"></div>
	</div>
</template>
```

css部分：

```css
.container {
    position: relative;
    display: flex;
    background: #fff;
    .left {
        display: flex;
        flex-direction: column;
        width: 20%;
        height: 86vh;
        padding: 15px 0 0;
        .left-resize {
          cursor: row-resize;
          height: 8px;
          background: #f0f2f5;
        }
        .left-tree {
          overflow-y: auto;
          height: 500px;
        }
        .left-table {
          margin-top: 10px;
          height: 100%;
        }
    }
    
    .right {
        width: 80%;
        position: relative;
    }
    
    .resize {
        cursor: col-resize;
        width: 10px;
        background: #f0f2f5;
      }
}
```

功能实现：

```vue
dragControllerDivVertical() {
    var resize = document.getElementsByClassName('resize')
    var left = document.getElementsByClassName('left')
    var mid = document.getElementsByClassName('right')
    var box = document.getElementsByClassName('inspection')
    let that = this

	for (let i = 0; i < resize.length; i++) {
        // 鼠标按下事件
        resize[i].onmousedown = function (e) {
          //颜色改变提醒
          resize[i].style.background = '#F0F2F5';
          var startX = e.clientX;
          resize[i].left = resize[i].offsetLeft;
          // 鼠标拖动事件
          document.onmousemove = function (e) {
            var endX = e.clientX;
            var moveLen = resize[i].left + (endX - startX); // （endx-startx）=移动的距离。resize[i].left+移动的距离=左边区域最后的宽度
            var maxT = box[i].clientWidth - resize[i].offsetWidth; // 容器宽度 - 左边区域的宽度 = 右边区域的宽度

            if (moveLen < 250) moveLen = 250; // 左边区域的最小宽度为250px
            if (moveLen > maxT - 550) moveLen = maxT - 550; //右边区域最小宽度为550px

            resize[i].style.left = moveLen; // 设置左侧区域的宽度

            if (that.selectedKeys.length) {
              if (moveLen > 500) {
                that.$refs.table.textLen = 8 + Math.ceil(moveLen / 100)
              } else {
                that.$refs.table.textLen = 6
              }
            }

            for (let j = 0; j < left.length; j++) {
              left[j].style.width = moveLen + 'px';
              mid[j].style.width = (box[i].clientWidth - moveLen - 10) + 'px';
            }
          };
          // 鼠标松开事件
          document.onmouseup = function (evt) {
            //颜色恢复
            resize[i].style.background = '#F0F2F5';
            document.onmousemove = null;
            document.onmouseup = null;
            resize[i].releaseCapture && resize[i].releaseCapture(); //当你不在需要继续获得鼠标消息就要应该调用ReleaseCapture()释放掉
          };
          resize[i].setCapture && resize[i].setCapture(); //该函数在属于当前线程的指定窗口里设置鼠标捕获
          return false;
        };
    }
}                              
```

mounted 时调用上面的方法。

# vue中实现拖动调整上下两侧div

样式都在之前。

功能实现：

```vue
dragControllerDivHorizon() {
    var resize = document.getElementsByClassName('left-resize')
    var left = document.getElementsByClassName('left-tree')
    var mid = document.getElementsByClassName('left-table')
    var box = document.getElementsByClassName('left')
    let that = this
    for (let i = 0; i < resize.length; i++) {
        // 鼠标按下事件
        resize[i].onmousedown = function (e) {
          var startY = e.clientY
          resize[i].top = resize[i].offsetTop
          // 鼠标拖动事件
          document.onmousemove = function (e) {
            var endY = e.clientY
            var moveLen = resize[i].top + (endY - startY) // endY-startY=移动的距离。resize.top+移动的距离=上面区域最后的高度
            var maxT = box[i].clientHeight - resize[i].offsetHeight // 容器高度 - 上面区域的高度 = 下面区域的高度

            if (moveLen < 200) moveLen = 200 // 上面区域的最小高度200px
            if (moveLen > maxT - 400) moveLen = maxT - 400 // 下面区域最小高度为400px
            resize[i].style.top = moveLen // 设置上面区域的高度

            left[i].style.height = moveLen + 'px';
            mid[i].style.height = (box[i].clientHeight - moveLen) + 'px';
            if (that.selectedKeys.length && box[i].clientHeight - moveLen > 300) {
              that.$refs.table.tableY = box[i].clientHeight - moveLen - 100
            }
          }
          // 鼠标松开事件
          document.onmouseup = function (evt) {
            //颜色恢复
            resize[i].style.background = '#F0F2F5'
            document.onmousemove = null
            document.onmouseup = null
            resize[i].releaseCapture && resize[i].releaseCapture() //当你不在需要继续获得鼠标消息就要应该调用ReleaseCapture()释放掉
          }
          resize[i].setCapture && resize[i].setCapture() //该函数在属于当前线程的指定窗口里设置鼠标捕获
          return false
        }
	}
}
```

参考文档：[vue中实现拖动调整左右两侧div的宽度](https://www.cnblogs.com/ingrid/p/12766457.html)