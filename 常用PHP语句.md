---
title: 常用 PHP 语句
date: 2018-04-30 19:55:32
tags: PHP
---

# 定义变/定量

* ```php
  define('author', 'Tom'); // 定量在所有地方都可以使用
  注意：
      a) 常量值不能改变
      b) 必须初始化值
      c) 区分大小写
      
  const('常量名', '常量值'); // 不能用于 if 和 函数中

  unset(); // 销毁变量
  ```

# 数组方面

- 新建一个数组

  - ```php
    $arr = array('html', 'css', 'JavaScript'); // 索引数组
    $arr = array('name' => 'Yamato', 'weapen' => '460mm 3 * 3'); // 关联数组
    ```

- 数组长度

  - ```php
    count($arr);
    ```

- 数组操作

  - ```php
    array_splice($lists, 0, 1); // 截取 第一个元素
    array_pop($arr); // 弹出最后一个单元
    array_push($arr, $v); // 类似 js 数组中的 push 方法
    array_keys($arr); // 将数组 $arr 的键以数组形式列出
    array_key_exists(); // 判断关联数组中是否存在某个键
    array_values($arr); // 将数组 $arr 的值以数组形式列出
    ```

- 数组遍历

  - ```php
    foreach($arr as $key => $val) {
        
    }
    // 索引/关联均用此方法
    ```

# 字符串方面

* 字符串操作

  * ```php
    // 通过 系统函数 mb_stripos 可以在某字符串中查找特定字符
    var_dump(mb_stripos($str, 'lilei', 0, 'utf8')); // 第三个参数表示从第几个开始找
    注意：
        a) 如果查找成功，则返回字符的位置
        b) 如果查找不成功，则返回 false
        c) 不区分大小写
        
    strlen(); // 获得字符串长度
    ```

# 输出

- echo  (最简单)
- print_r
- var_dump (最详细)

# 时间戳

* time()；

* 系统函数 date 可以对时间戳进行 格式化 处理

  * ```php
    date('Y', time());
    date('m', time());
    date('d', time());
    date('Y-m-d', time());
    ```

# 文件处理

```php
$txt = file_get_contents('./test.txt'); // 获取文件
file_put_contents('./storage.json', json_encode($lists)); // 写入文件 
注意：
    a) 当要写入内容的文件不存在时，会自动创建这个文件
    b) 写入文件时，默认是覆盖方式
    c) 通过系统常量 FILE_APPEND 可以指定写放文件的方式为 追加方式 
    	file_put_contents('test.txt', '以追加方式添加新内容', FILE_APPEND);

move_uploaded_file($_FILES['avatar']['tmp_name'], './form/uploads/' . $_FILES['avatar']['name']); // 移动上传上来的文件 可以长期保存 第一个参数是 文件本身 第二个参数是 要存放的文件路径
注意：
     由于 Windows 系统使用 GBK 编码
	// 而 PHP 代码中在处理时使用 UTF-8
	// 必须通过系统函数 iconv 进行转换
	// 检测文本编码
	echo mb_detect_encoding($_FILES['source']['name']);
	// 进行编码转换时，出现了问题（bug）
	$name_gbk = iconv('UTF-8', 'GBK', $_FILES['source']['name']);
	$path = './upload/' . $name_gbk;

$lists = json_decode($json, true); // 将 json 转为数组 第二个参数，并且值为 true 会强制转为数组
$json = json_encode($arr); // 将数组转为 json
include './include.php'; // 导入一个外部文件（非必须）
require './require.php'; // 导入一个外部文件（必须）
```

# 字符串与数组之间的转换

```php
$arr = explode("\n", $tex); // 字符串变为数组
$str = implode("|", $_POST); // 数组变为字符串
```

# 前后交互时用到

```php
$_GET // 前台用 get 方式向后台传输参数
$_POST // 前台用 post 方式向后台传输参数
$_SERVER['REQUEST_METHOD'] // 可在后台获取前台向后台传递参数的方式
$_SERVER['HTTP_USER_AGENT']; // 客户端浏览器信息
$_FILE // 前台有 input 上传文件时，在后台获取文件信息 是数组形式
```

# 响应头的设置

* 跳转

  * ```php
    header('Refresh: 2; url=./index.php'); //停留2秒后跳转至index.php
    ```

* 文件编码，形式

  * ```php
    header('Content-Type: text/html; charset=UTF-8');
    header('Content-Type: text/css');
    header('Content-Type: text/javascript');
    header('Content-Type: application/json');
    header('Location: http://www.baidu.com'); // 重定向
    header('Content-Type: application/octet-stream');
    header('Content-Disposition: attachment; filename=2.png');
    header('Access-Allow-Control-Origin:*'); // cors解决跨域
    ```

# 判断值

* isset

  * ```php
    $name = '';
    var_dump(isset($name)); // true
    注意：
        a) isset 是用来检测变量是否有值，而不是检测变量是否存在
        b) 当值为 null 等同于无值
    ```

* empty

  * ```php
    // 系统函数 empty 检测某个变量是否为 空
    $str = '';
    var_dump(empty($str)); // true
    注意：
        a) 字符串 '' 返回 true
        b) 数组 array() 返回 true
        c) 数值 0 返回 true
    ```

# 数据库操作

```php
$connect = mysqli_connect('127.0.0.1', '用户名', '密码'); // 连接 mysql
mysqli_select_db($connect, 'posts'); // 连接指定库
mysqli_query($connect, $sql); // 识别 SQL 语句
$res = mysqli_fetch_assoc($res); // 将查询结果转为数组
注意： 通常这样使用
    $rows = array();
	while ($row = mysqli_fetch_assoc($res)) {
		array_push($rows, $row);
	}
mysqli_error($connect); // 通过 mysqli_error 函数，可以得知数据库操作的错误信息
```

# session 与 cookie

```php
session_start(); // 使用 session 前(获取和设置)要开启 sessio
setcookie('name', 'itcast'); // PHP 中使用 setcookie 函数，也可以对cookie 进行一个 间接的 设置。通过 								响应头 Set-Cookie 要求（指示）浏览器设置相应的 cookie
$_SESSION['name'] = null; // 销毁一个 session
unset($_SESSION['name']); // 销毁一个 session
```

# 其他

```php
sleep(3); // 延时 3 秒再执行
trim($val[0]); // 去除字符串两端的空格
exit(); // 程序停止，不执行下方的代码
die(); // 程序停止，退出当前代码
@mysqli_connect('127.0.0.1', 'root', 'root'); // @ 不会解决错误，只是让错误不显示出来
path // 控制 cookie 的访问级别，默认只有在当前目录与子目录下可以被访问
domain // 控制 cookie 的子域访问级别
max-age // 控制 cookie 的过期时间，使用秒数，表示多长时间后过期
epeires // 控制 cookie 的过期时间，使用 Date 来描述什么时候过期  
```

