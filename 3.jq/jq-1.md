## jquery

*2022.3.10*

### 1.杂项

自己封装

### 2.一些属性

#### 2.1文档处理

1. `a.append(b)` 把b添加到 a节点内部最后

   `a.appendTo(b)` 把a添加到b节点内部最后

2. `prepend()` `prependTo()` 与前相反，到前面

3. `a.after(b)`  把b添加到a节点外部之后，同级

   `a.insertAfter(b)` 把a添加到b节点外部之后，同级

4. `before()` `insertBefore` 与前相反，到前面

5. `clone(boolean)` 是否复制其事件处理函数



#### 2.2选择器

1. :not(［属性])

   排除带有某属性的节点，选中其他

2. `：has(x)` 选择包含x元素的元素

3.  `[attribute=value]` 选择属性名 = 属性值 的元素

4. 
