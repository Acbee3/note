---
title: 常用 Web API
tags: api
data: 2018-04-10
---

## 常用语句

### 元素的创建与追加

```javascript
var node = document.createElement( '标签名' );
父节点.appendChild( 子节点 );
父节点.insertBefore( 子节点, 原有节点 ); // 插在原有节点的前面
```



### 获取元素

```javascript
document.getElementById();  // 单个元素
document.getElementsByTagName();
document.querySelector(); // 单个元素
document.querySelectorAll();
document.getElementsByClassName();
document.getElementByName('name'); // 有兼容问题 一般不用
```



### 样式操作(javascript只能改变行内样式)

```javascript
dom对象.setAttribute('class', '类名') // 可用于自定义属性  DOM Core
dom对象.getAttribue('属性名')
dom对象.className = ''; // 由于 class 是关键字，不能直接用   HTML DOM
dom对象.style.backgroundColor | width | height ... = '';
element.style.样式属性 // 读取
window.getComputedStyle('元素名'); // 只能读取 可以读取嵌入的样式 
```



### 节点操作

```javascript
dom对象.parentNode; // 任何元素的父元素只有一个
dom对象.childNodes;
dom对象.firstChild;
dom对象.lastChild;
dom对象.nextSibling; // 下一个兄弟节点；
dom对象.previousSibling; // 上一个兄弟节点；
dom对象.nextElementSibling; // 下一个DOM兄弟节点（不包括文本节点）；
dom对象.previousElementSibling; // 上一个DOM兄弟节点（不包括文本节点）；

创建元素的三种方式：
	document.createElement('标签名'); // 创建标签节点；
	box.innerHTML = '新内容<p>新标签</p>'; // 创建标签节点；
	document.write('新设置的内容<p>标签也可以生成</p>'); // 创建标签节点；

父节点.appendChild(子节点); // 在父节点中追加子节点，按添加的顺序，默认直接加到已有的最后面；
父节点.removeChild(子节点); // 移除
父节点.insertBefore(新节点, 原有节点);  // 将新的节点插入到原有节点的前面
element.innerHTML = ''; // 可以识别dom 改变类样式 其取值也会识别dom 用<>时 要用 &lt; 和 &gt;
element.innerText       // 不识别dom 把一切都变为 字符串 取值 也是全部取下来 不改变内容
```



### 类名操作

```javascript
dom对象.classList.add('class'); // 添加类名
dom对象.classList.remove('class'); // 移除类名
dom对象.classList.toggle('class'); // 有则去掉，无则添加 不影响其他类名
dom对象.classList.contains('class'); // 检测是否存在class
```



### 事件操作

```javascript
dom对象.onclick = function () {};
dom对象.onmouseover // 会触发冒泡
dom对象.onmouseout // 会触发冒泡
dom对象.onmouseenter // 不产生冒泡
dom对象.onmouselesve // 不产生冒泡
dom对象.onmousemove
dom对象.ondblclick
dom对象.onkeydown
dom对象.onkeyup
dom对象.onkeypress
element.addEventListener('事件名', 事件处理函数, [配置]) // 可以追加多个事件 配置与取消冒泡有关
element.removeEventListener('事件名', 事件处理函数) // 移除事件 以上两个均可以取消冒泡 是新方法
element.attachEvent('onclick', function() {}); // IE8 中用于事件的追加
element.detachEvent()

window.onscroll // 滚动是 window 去触发 浏览器滚动条滚动事件
document.onmousewheel // 鼠标滚轮事件

```



### 取消事件冒泡

```javascript
window.event.cancelBubble = true; // 默认是 false 不取消冒泡
e.stopPropagation();
dom元素.addEventListener('事件名', 事件处理函数, 配置); // 配置为boolean值，默认为 false, 表示冒泡，													  设置为 true 表示捕获
```



### 数组提供的遍历方法

```javascript
arr.forEach(function() {}); // 将每一个数组元素都取出来一个一个进行函数处理
arr.map(function() {}); // 对每一个元素在原有基础上进行“样式”上的操作
arr.filter(function() {}); // 对每一个元素进行筛选 返回符合条件的元素
```



### 数组的方法

```javascript
length 属性 动态获取数组长度
join(); // 将数组转成字符串 返回一个字符串
reverse(); // 将数组中各元素颠倒顺序
delete // 只能删除数组元素的值 但所占空间还在 总长度不变(arr.length)
shift(); // 删除数组中第一个元素 返回删除的那个值 并将长度减1
pop(); // 删除数组中最后一个元素 返回删除的那个值 并将长度减1
unshift(); // 往数组前面添加一个或多个数组元素 长度要改变 arrObj.unshift('a', 'b', 'c');
push(); // 往数组结尾添加一个或多个数组元素 长度要改变
concat(); // 连接数组
slice(); // 返回数组的一部分 用下标索引 （下标可以取负数）
sort(); // 对数组进行排序
splice(); // 插入 删除 替换 数组中的元素
toString(); // 数组转字符串
indexOf(); // 在数组中查找元素
findIndex(); // 根据元素找索引 与 filter map 一样 自带遍历
Array.from(arrayLike[, mapFn[, thisArg]]) // 从一个类似数组或可迭代对象中创建一个新的数组实例
```



### 字符串方法

```javascript
字符串的不可变性：
	每一个看起来会修改String值得方法，其实是创建了一个新的String实例， 
	用来包含修改之后的内容，而最初的String实例没有改变

charAt(index); // 从一个字符串中返回指定的字符
str.charCodeAt(index) // 获取指定位置处字符的Unicode码
String.fromCharCode(num1, ..., numN) // 根据Unicode码返回对应的字符
str[0] // 与 charAt() 一样
str.concat(string2, string3[, ..., stringN]) // 和原字符串连接的多个字符串
str.slice(beginSlice[, endSlice]) // 从start位置开始，截取到end位置，end取不到  可以取负数
str.substr(start[, length]) // 从start位置开始，截取length个字符
str.substring(indexStart[, indexEnd]) // 从start位置开始，截取到end位置，end取不到  不能取负数,负数按0处理
str.indexOf(searchValue[, fromIndex]) // 返回指定内容在元字符串中的位置 没有返 -1
str.lastIndexOf(searchValue[, fromIndex]) // 从后往前找，只找第一个匹配的
str.includes(searchString[, position]) // 是否（在某个位置）包含某个字符串
str.trim() // 只能去除字符串前后的空白 返回一个新的字符串
str.replace(regexp|substr, newSubStr|function) // 字符串替换
str.search(regexp) // 返回值类似 indexOf()
str.split([separator[, limit]]) // 常用来字符串转数组
str.toString() // 将其他类型的数据转为 字符串
str.padStart(targetLength [, padString]) // 'abc'.padStart(8, "0");  "00000abc"
str.padEnd(targetLength [, padString]) // 'abc'.padEnd(6, "123456");  "abc123"
str.startsWith(searchString [, position]); // str.startsWith("not to be", 10) 类似 includes
str.endsWith(searchString [, length]); // startsWith() 反过来
str.toUpperCase() // 转为大写
str.toLowerCase() // 转为小写
```



### Math方法

```javascript
Math.abs(x); // 绝对值
Math.PI // 圆周率
Math.ceil(x) // 向上取整
Math.floor(x) // 向下取整
Math.max([value1[,value2, ...]]) // 返回给定的一组数字中的最大值 有不是数字的 返回 NaN
Math.min([value1[,value2, ...]]) // 给定数值中最小的数
Math.random() // 一个浮点型伪随机数字在0（包括0）和1（不包括）之间
Math.round(x) // 四舍五入
Math.round(Math.random()*(y-x)+x)  // 返回从x到y之间的随机数 包括 x 不包括 y
function getRandomIntInclusive(min, max) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min + 1)) + min; //The maximum is inclusive and the minimum is inclusive 
}
// 包括x与y
```



### 计时器

```javascript
var timer = set.setInterval(函数, 时间间隔);
```



### load事件

```javascript
window.load = function() {
    
}
// 将 js 代码放到 html 代码之前要加这段代码 表示要在页面加载完成后执行 js
```



### 时间

```js
var timer = new Date()
    timer.getTime(); // 时间戳
    timer.valueOf(); // 时间戳
    Date.now(); // 时间戳
    + new Date(); // 时间戳

var time = new Date(); // 返回当日的日期和时间
var date = time.getDate(); // 从 Date 对象返回一个月中的某一天 (1 ~ 31)
var day = time.getDay(); // 从 Date 对象返回一周中的某一天 (0 ~ 6)
var mon = time.getMonth(); // 从 Date 对象返回月份 (0 ~ 11) 使用时要 + 1
var year= time.getFullYear(); // 从 Date 对象以四位数字返回年份
var hour = time.getHours(); // 返回 Date 对象的小时 (0 ~ 23)
var min = time.getMinutes(); // 返回 Date 对象的分钟 (0 ~ 59)
var sec = time.getSeconds(); // 返回 Date 对象的秒数 (0 ~ 59)
var mill = time.getMilliseconds(); // 返回 Date 对象的毫秒(0 ~ 999)

时： Math.floor(t%86400%3600);
分： Math.floor(t%86400%3600/60);
秒： Math.floor(t%60);
```



### 处理JSON格式

```javascript
JSON.parse(); // 将 json 格式转为数组(json为[])或对象(json为{})
JSON.stringify(); // 将数组或对象转为 json 格式
```



### Cookie

```javascript
document.cookie = 'age=16'; // 设置Cookie
document.cookie; // 获取所有的Cookie
```



### 全屏操作（html5 新增）

```javascript
由于是 html5 新增的 API ，所以并不是所有的浏览器都支持这个方法，不同浏览器要加浏览器前缀
元素对象.webkitRequestFullScreen(); // 使这个元素对象全屏(谷歌)
	webkit- // 谷歌
    moz- // 火狐
    o- // 欧鹏
    ms- // ie(但不支持)
document.webkitCancelFullScreen(); // (谷歌)退出全屏(固定格式)
document.webkitCancelFullScreen； // 是谷歌浏览器则返回一个函数 ƒ webkitRequestFullScreen() { 									[native code] }，不是则返回undefined (用于对不同浏览器判断全屏)
document.webkitFullscreenElement; // 返回全屏元素对象，没有返回 null (谷歌 's' 小写)
document.mozFullScreenElement; // 火狐 's' 大写
```

### 自定义属性

```html
<div data-abc="what"></div>
推荐用 data-* 的写法
dom对象.dataset['abc']; // 读取自定义属性 abc 的值
dom对象.dataset['abc'] = 'prama'; // 设置自定义元素 abc 的值
如果<div data-big-surp="gift"></div>
dom对象.dataset['bigSurp]; // 用驼峰命名

jQuery 中用 对象.data('abc');
```



### 多媒体

> 自定义播放器

方法

| 方法           | 描述                                    |
| -------------- | --------------------------------------- |
| addTextTrack() | 向音频/视频添加新的文本轨道             |
| canPlayType()  | 检测浏览器是否能播放指定的音频/视频类型 |
| load()         | 重新加载音频/视频元素                   |
| play()         | 开始播放音频/视频                       |
| pause()        | 暂停当前播放的音频/视频                 |

属性

| 属性                | 描述                                                       |
| ------------------- | ---------------------------------------------------------- |
| audioTracks         | 返回表示可用音轨的 AudioTrackList 对象                     |
| autoplay            | 设置或返回是否在加载完成后随即播放音频/视频                |
| buffered            | 返回表示音频/视频已缓冲部分的 TimeRanges 对象              |
| controller          | 返回表示音频/视频当前媒体控制器的 MediaController 对象     |
| controls            | 设置或返回音频/视频是否显示控件（比如播放/暂停等）         |
| crossOrigin         | 设置或返回音频/视频的 CORS 设置                            |
| currentSrc          | 返回当前音频/视频的 URL                                    |
| **currentTime**     | **设置或返回音频/视频中的当前播放位置（以秒计）**          |
| defaultMuted        | 设置或返回音频/视频默认是否静音                            |
| defaultPlaybackRate | 设置或返回音频/视频的默认播放速度                          |
| **duration**        | **返回当前音频/视频的长度（以秒计）**                      |
| ended               | 返回音频/视频的播放是否已结束                              |
| error               | 返回表示音频/视频错误状态的 MediaError 对象                |
| loop                | 设置或返回音频/视频是否应在结束时重新播放                  |
| mediaGroup          | 设置或返回音频/视频所属的组合（用于连接多个音频/视频元素） |
| muted               | 设置或返回音频/视频是否静音                                |
| networkState        | 返回音频/视频的当前网络状态                                |
| **paused**          | **设置或返回音频/视频是否暂停**                            |
| playbackRate        | 设置或返回音频/视频播放的速度                              |
| played              | 返回表示音频/视频已播放部分的 TimeRanges 对象              |
| preload             | 设置或返回音频/视频是否应该在页面加载后进行加载            |
| readyState          | 返回音频/视频当前的就绪状态                                |
| seekable            | 返回表示音频/视频可寻址部分的 TimeRanges 对象              |
| seeking             | 返回用户是否正在音频/视频中进行查找                        |
| src                 | 设置或返回音频/视频元素的当前来源                          |
| startDate           | 返回表示当前时间偏移的 Date 对象                           |
| textTracks          | 返回表示可用文本轨道的 TextTrackList 对象                  |
| videoTracks         | 返回表示可用视频轨道的 VideoTrackList 对象                 |
| volume              | 设置或返回音频/视频的音量                                  |

事件

| 事件           | 描述                                         |
| -------------- | -------------------------------------------- |
| abort          | 当音频/视频的加载已放弃时                    |
| **canplay**    | **当浏览器可以播放音频/视频时**              |
| canplaythrough | 当浏览器可在不因缓冲而停顿的情况下进行播放时 |
| durationchange | 当音频/视频的时长已更改时                    |
| emptied        | 当目前的播放列表为空时                       |
| ended          | 当目前的播放列表已结束时                     |
| error          | 当在音频/视频加载期间发生错误时              |
| loadeddata     | 当浏览器已加载音频/视频的当前帧时            |
| loadedmetadata | 当浏览器已加载音频/视频的元数据时            |
| loadstart      | 当浏览器开始查找音频/视频时                  |
| pause          | 当音频/视频已暂停时                          |
| play           | 当音频/视频已开始或不再暂停时                |
| playing        | 当音频/视频在已因缓冲而暂停或停止后已就绪时  |
| progress       | 当浏览器正在下载音频/视频时                  |
| ratechange     | 当音频/视频的播放速度已更改时                |
| seeked         | 当用户已移动/跳跃到音频/视频中的新位置时     |
| seeking        | 当用户开始移动/跳跃到音频/视频中的新位置时   |
| stalled        | 当浏览器尝试获取媒体数据，但数据不可用时     |
| suspend        | 当浏览器刻意不获取媒体数据时                 |
| **timeupdate** | **当视频的播放位置更改时**                   |
| volumechange   | 当音量已更改时                               |
| waiting        | 当视频由于需要缓冲下一帧而停止               |

### 文件读取

```javascript
// 常用在上传图片预览上
file.onchange = function () {
	// console.log(this.files[0]);
			
	var fileimg = this.files[0];  
			
	var reader = new FileReader();
			
	reader.readAsDataURL(fileimg);
			
	reader.onload = function () {
		var img = document.createElement('img');
		img.src = reader.result;
		console.log(reader.result); // 文件本身
		box.appendChild(img);
	}
}
```



### 本地存储

```javascript
(window).localStorage.setItem('key', 'value'); // 设置数据
(window).localStorage.getItem('key'); // 获取特定的数据
(window).localStorage.removeItem('key'); // 移除特定的数据
clear(); // 清除所有数据

永久生效，除非手动删除（服务器方式访问然后清除缓存）
可以多窗口（页面）共享（同一域名下）
```



