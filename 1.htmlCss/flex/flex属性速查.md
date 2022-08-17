## 父容器上的属性

1. `flex-direction` 主轴的方向 
   1. row 
   2. row-reverse 
   3. column 
   4. column-reverse
2. `flex-wrap` 是否换行 
   1. nowrap 
   2. wrap 
   3. wrap-reverse
3. `flex-flow` 前两个的简写，接收两个值
4. `justify-content ` 主轴上的对齐方式
   1. flex-start 靠左
   2. flex-end 靠右
   3. center 居中
   4. space-between 两端对齐，子项间距相等
   5. space-around 两个子项中的间隔相等，距离左右边框的距离为两项距离的一般
5. `align-items` 交叉轴上的对齐方式
   1. flex-start 顶部对齐
   2. flex-end 底部对齐
   3. center
   4. stretch 拉伸，占满整个容器高度
   5. baseline 子项的第一行文字基线对齐
6. `align-content` 多根轴线时的对齐方式
   1. flex-start
   2. flex-end
   3. center
   4. strentch
   5. space-between
   6. space-around



## 子容器上的属性

1. `order` 子项的排列顺序，越小越考前
2. `flex-grow` number 按比例分配剩余空间
3. `flex-shrink` number 空间不足时，按比例缩小
4. `flex-basis` px，百分比 auto  在分配多余空间前，子项本身大小(auto表示用子项本来的大小)
5. `flex` 前三个的集合 默认 0 1 auto
   1. auto == 1 1 auto
   2. none == 0 0 auto
6. `align-self` 指定某个子项单独的对齐方式，覆盖`align-item` 属性
   1. stretch 默认继承父元素的 `align-item` 属性，没有的话就拉伸
   2. flex-start
   3. flex-end
   4. center
   5. baseline
   6. strentch