# jQuery

## 常用语句（大多是方法，只有极少数的属性）

### 入口函数

```	javascript
$(function() {
    
});
或
$(document).ready(function() {
    
});
// window.onload只能注册一次，jQuery入口函数可以注册多次
```

### DOM 对象 与 jQuery 对象 的转化

```javascript
DOM => jQuery
$(dom对象)；
jQuery => DOM
jQuery对象[索引值];
jQuery对象.get(索引值);
```

### 选择器

```javascript
$('#id');
$('.className');
$('div');
$('ul li');
$('ul > li');
$('div, p, span');
$('div.class');
$('li:eq(2)').css('color', 'red'); // 从0开始
$('li:odd').css('color', 'red');  // 索引 为 奇数
$('li:even').css('color', 'red'); // 索引 为 偶数
$('ul').children('li'); // 相当于 $('ul > li');
$('ul').find('li'); // 相当于 $('ul li');
$('#first').siblings(); // 查找其兄弟节点 不包括自身
$('#first').parent(); // 父节点 （只有一个）
$('#sirst').parents('div'); // 父节点中的 div
$('li').eq(2); // 相当于 $('li:eq(2)');
$('li').next(); // 找下一个兄弟
$('li').prev(); // 找上一个兄弟
```

### 样式操作

```javascript
$obj.css('color', 'red');
$obj.css({
    'color': 'red',
    'backgroundColor': 'blue'
})  // 设置多个样式
$obj.css('backgroundColor'); // 获取样式
```

###class操作

```javascript
$obj.addClass();
$obj.removeClass();
$obj.hasClass();
$obj.toggleClass();
```

### attr操作(应用范围最广，类名，id名，style样式都可以操作)

```javascript
$obj.attr('title', '点击图片');
$obj.attr({
    title:'哎哟，不错哦',
    alt:'哎哟，不错哦',
    style:'opacity:.5'
})  
$obj.attr('title');
$('img').removeAttr('title'); // 移除属性
```

### prop操作(对于checked selected disabled 这类布尔类型的属性)

```javascript
$(':checked').prop('checked', true); // 设置
$obj.prop('checked'); // 获取
```

### val()/text/()html()

```javascript
$obj.val()		// 获取或者设置表单元素的value属性的值
$obj.html() 	// 对应innerHTML
$obj.text()		// 对应innerText/textContent，处理了浏览器的兼容性
```

### jQuery动画

```javascript
$obj.show([speed], [callback]);
// speed(可选)：动画的执行时间
	 // 1.如果不传，就没有动画效果。如果是slide和fade系列，会默认为normal
	 // 2.毫秒值(比如1000),动画在1000毫秒执行完成(推荐)
     // 3.固定字符串，slow(600)、normal(400)、fast(200)，如果传其他字符串，则默认为normal。
// callback(可选):执行完动画后执行的回调函数
slideDown()/slideUp()/slideToggle();同理
fadeIn()/fadeOut()/fadeToggle();同理

$(selector).animate({params},[speed],[easing],[callback]);
// {params}：要执行动画的CSS属性，带数字（必选）
// speed：执行动画时长（可选），默认400
// easing:执行效果，默认为swing（缓动）慢快慢  可以是linear（匀速）
// callback：动画执行完后立即执行的回调函数（可选）

// stop方法：停止动画效果
stop(clearQueue, jumpToEnd);
// 第一个参数：是否清除队列
// 第二个参数：是否跳转到最终效果
```

### jQuery节点操作

#### 创建节点

```javascript
$('<span>这是一个span元素</span>');
```

#### 添加节点

```javascript
父节点.append(子节点);
子节点.appendTo(父节点); // 在被选元素的结尾插入内容
父节点.prepend(子节点);  
子节点.prependTo(父节点); // 在被选元素的开头插入内容
节点.before();  // 在被选元素之后插入内容
节点.after();  // 在被选元素之前插入内容
```

#### 清空节点与删除节点

```javascript
$('div').empty(); // 清空div的所有内容（推荐使用，会清除子元素上绑定的内容，源码）但自身保留
$('div').html('');// 使用html方法来清空元素 赋值操作
$('div').remove(); // 相比于empty，自身也删除
```

#### 克隆节点

```javascript
// 复制$(selector)所匹配到的元素（深度复制）
// cloneNode(true)
// 返回值为复制的新元素，和原来的元素没有任何关系了。即修改新元素，不会影响到原来的元素。
$(selector).clone();
```

### jQuery尺寸和位置操作

#### width方法与height方法

```javascript
// 带参数表示设置高度
$('img').height(200);
// 不带参数获取高度
$('img').height();
// 获取可视区宽度
$(window).width();
// 获取可视区高度
$(window).height();
innerWidth()/innerHeight()	// 方法返回元素的宽度/高度（包括内边距）。
outerWidth()/outerHeight()  // 方法返回元素的宽度/高度（包括内边距和边框）。
outerWidth(true)/outerHeight(true)  // 方法返回元素的宽度/高度（包括内边距、边框和外边距）。

// 获取页面被卷曲的高度
$(window).scrollTop();
// 获取页面被卷曲的宽度
$(window).scrollLeft();

// 设置滚动动画(必须是body, html)
$('body,html').animate({
    scrollTop: 0
}, 100)

// 获取或设置元素距离document的位置,返回值为对象：{left:100, top:100}
$(selector).offset();
// 获取相对于其最近的有定位的父元素的位置。
$(selector).position();
```

### jQuery事件机制

#### 事件绑定

```javascript
// 注册多个事件
$(selector).bind('click mousemove', function() {
    
})
// 注册委托事件
$(selector).delegate('p', 'click', function() {
    
})
// 综合(重要)
$(selector).on('mouseover click', 'p', function() {
    
})
// 第一个参数：events，绑定事件的名称可以是由空格分隔的多个事件（标准事件或者自定义事件）
// 第二个参数：selector, 执行事件的后代元素（可选），如果没有后代元素，那么事件将有自己执行。
// 第三个参数：data，传递给处理函数的数据，事件触发的时候通过event.data来使用（不常使用）
// 第四个参数：handler，事件处理函数
$(selector).on(events[,selector][,data],handler);
```

#### 事件解绑

```javascript
$(selector).unbind(); // 解绑所有的事件
$(selector).unbind('click'); // 解绑指定的事件
$(selector).undelegate(); // 解绑所有的delegate事件
$(selector).undelegate('click'); // 解绑所有的click事件

// 重要
// 解绑匹配元素的所有事件
$(selector).off();
// 解绑匹配元素的所有click事件
$(selector).off('click');
```

#### 触发事件

```javascript
$(selector).click(); // 触发 click事件 用代码触发 不是手动
$(selector).trigger('click');

$(selector).hover(fnEnter, fnLeave);
// 下面的简写形式
$(selector).mouseenter(function () {
}).mouseleave(function () {
})
```

#### jQuery事件对象

```javascript
 screenX和screenY	// 对应屏幕最左上角的值
 offsetX和offsetY  // 获取鼠标在元素中的位置
 clientX和clientY	// 距离页面左上角的位置（忽视滚动条） pageX和pageY	距离页面最顶部的左上角的位置（会计算滚动条的距离）

 event.keyCode	// 按下的键盘代码
 event.data	// 存储绑定事件时传递的附加数据

 event.stopPropagation()	// 阻止事件冒泡行为
 event.preventDefault()	// 阻止浏览器默认行为
 return false; // 既能阻止事件冒泡，又能阻止浏览器默认行为。
```

### each方法

```javascript
// 参数一表示当前元素在所有匹配元素中的索引号
// 参数二表示当前元素（DOM对象）
$(selector).each(function(index,element){});
```

### 多库共存

```javascript
var c = $.noConflict();// 释放$的控制权,并且把$的能力给了c
```

### 循环遍历

```javascript
$(selector).each(function(i, v) {
    
});
$.each(arr, function(i, v) {
    
})
```

### 表单的事件

```javascript
$(selector).serialize(); // 输出标准的查询字符串 a=1&b=2&c=3&d=4&e=5
```

