### 1.父元素relative，子元素absolute + 负margin

---

#### 缺点：必须要知道子元素的宽高

```html
<div class="wp">
    <div class="box size">123123</div>
</div>
```

```css
/* 公共代码 */
.wp {
    border: 1px solid red;
    width: 300px;
    height: 300px;
}

.box {
    background: green;    
}

.box.size{
    width: 100px;
    height: 100px;
}
/* 公共代码 */
```

**绝对定位的百分比是相对与脱离文档流的父元素的宽高**

```css
/* 此处引用上面的公共代码 */
/* 此处引用上面的公共代码 */

/* 定位代码 */
.wp {
    position: relative;
}
.box {
    position: absolute;;
    top: 50%;
    left: 50%;
    margin-left: -50px;	/*50是子元素自己宽度的一半*/
    margin-top: -50px;
}
```



### 2.父元素relative，子元素absolute + margin auto

---

#### 缺点：需要知道子元素宽高

这种方式通过设置各个方向的距离都是0，此时再讲margin设为auto，就可以在各个方向上居中了

```html
<div class="wp">
    <div class="box size">123123</div>
</div>
```

```css
/* 此处引用上面的公共代码 */
/* 此处引用上面的公共代码 */

/* 定位代码 */
.wp {
    position: relative;
}
.box {
    position: absolute;;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    margin: auto;
}
```



### 3.absolute + calc

---

#### 缺点：兼容性依赖calc的兼容性，缺点是需要知道子元素的宽高

这种方式也要求居中元素的宽高必须固定

```html
<div class="wp">
    <div class="box size">123123</div>
</div>
```

css3带来了计算属性，既然top的百分比是基于元素的左上角，那么在减去宽度的一半就好了

```css
/* 此处引用上面的公共代码 */
/* 此处引用上面的公共代码 */

/* 定位代码 */
.wp {
    position: relative;
}
.box {
    position: absolute;;
    top: calc(50% - 50px);
    left: calc(50% - 50px);
}
```

