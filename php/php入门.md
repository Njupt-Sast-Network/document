PHP入门教程
=========================
>PHP 是一种创建动态交互性站点的强有力的服务器端脚本语言，本文档将会介绍一些基础的PHP知识。学习完成本教程后，将获得建立简单动态网站的能力。本文档需要一点点HTML的基础知识，可以先参考这篇[前端入门文档](https://github.com/Njupt-Sast-Network/document/blob/master/fem/fem入门那点小事/home.md)。

##简介
PHP的全称为：PHP：Hypertext Preprocessor，即“PHP：超文本预处理器”，是一种开源的通用计算机脚本语言，尤其适用于网络开发并可嵌入HTML中使用。易于学习，入门简单是其特点之一。

客户端在向web服务器请求php页面的时候，服务器上的php解析器通过运行php脚本中的php代码来生成纯html页面，并将其传输给客户端。最终客户端收到的html页面中将不包含php代码。若需要在自己的电脑上进行php开发，就需要在电脑上安装php解析器。

通常，类似于[XAMPP](https://www.apachefriends.org/zh_cn/index.html)这样的建站集成包会整合web开发所需的软件（Apache网页服务器+PHP+MySQL数据库），因此在Windows下只需安装XAMPP即可获得能够运行php的环境。Mac系统和Linux系统<!-- 待填坑 -->

##一点准备
php的所有代码，都包含在`<?php`和`?>`之间，像这样：

```php
<?php
for ($number = 1; $number <= 10; $number++) {
	if ($number <= 9) {
		echo $number . ", ";
	} else {
		echo $number . "!";
	}
};
?>
```

由于php解析器只会解析在`<?php`和`?>`之间的代码，因此php代码也可以被嵌入在HTML代码之中,并出现在任意位置。

```html
<!DOCTYPE html>
<html>
	<head>
	</head>
	<body>
        <p>
          <?php
            echo "Hello,World";
          ?>
        </p>   
	</body>
</html>

```
最终浏览器收到的HTML文档中将不会包含php代码，只会有解析结果`Hello,World!`。

如果现在看不懂这些代码也没有关系，下面我们会从头开始。

##Getting Started

>注：以下假定使用的是windows系统，并以默认设置安装了XAMPP。其他建站包和操作系统请自行参考其他文档。

首先我们在web根目录（通常是C:\xmapp\htdocs）下新建一个空白文本文档，并命名为index.php

>如果新安装了XAMPP,htdocs会包含一些附带的示例页面，请先将这些页面删除或者移到其他地方。此外Windows默认会隐藏文件后缀名，注意不要创建为index.php.txt这样的文件

使用文本编辑器（推荐[Sublime Text](http://www.sublimetext.com/)）打开这个文件，并如下输入：

```php
<?php
	echo "Hello,World";
?>
```

和C语言类似，每个php语句以分号`;`结尾。

echo函数会输出字符串，php中字符串以一对双引号包围。

保存这个文件，打开XAMPP的控制面板并启动Apache网页服务器（它会调用php解析引擎），打开浏览器并在地址栏输入`127.0.0.1`，回车。

>注：`127.0.0.1`这个被称为“本地环回”的特殊的IP地址会指向本机上的服务，输入`localhost`也有一样的效果。


>如果在XAMPP中无法启动Apache，并且看到了类似于这样的提示：

```
21:48:34  [Apache] 	Problem detected!
21:48:34  [Apache] 	Port 443 in use by ""C:\Program Files (x86)\VMware\VMware Workstation\vmware-hostd.exe" -u "C:\ProgramData\VMware\hostd\config.xml"" with PID 1956!
21:48:34  [Apache] 	Apache WILL NOT start without the configured ports free!
21:48:34  [Apache] 	You need to uninstall/disable/reconfigure the blocking application
21:48:34  [Apache] 	or reconfigure Apache and the Control Panel to listen on a different port

```

>那么说明VMWare占用了Apache使用的443端口，请前往VMWare的首选项->共享虚拟机中禁用共享，或者改用其他空闲端口。


如果一切正常的话，应该能在浏览器中看到我们~~喜闻乐见~~的Hello,World了。
![喜闻乐见的Hello,World](https://raw.githubusercontent.com/Njupt-Sast-Network/document/master/php/pic/gettingstarted1.png)

如果看到了`Hello,World`，那么恭喜你，你已经成功地写出了第一个php页面。

##字符串和数值
echo函数用来输出字符串（我们刚才其实已经见到过了）

例如
```php
<?php 
	echo "Hello, World"; 
?>
```

可以使用英文句点`.`来连接字符串，例如

```php
<?php
	echo "the quick brown fox"." jumps over "."the lazy dog";
?>;
```

>如果之前接触过JavaScript, 那么其实对于字符串来说，这个句点在php的和JS中的加号`+`的作用是一样的

既然是程序语言，那么必然少不了数值运算。

```php
<?php
	echo 1000-7;
	echo 12.34*56.78;
	echo 2**10;
?>
```
>php使用`**`来表示幂，例如`2**10`代表2的10次方，也就是1024

很简单不是么？

##变量
变量是存储数据的容器。先看下面的例子：
```php
<?php
	$x=5;
	$y=6;
	$z=$x+$y;
	echo $z;
?>
```
机智的你会猜到，结果会输出11。

正如在初中代数中那样，
```
x=5
y=6
z=x+y
```
我们使用变量来保存数据。
在php中，上面的`$x`,`$y`,`$z`被称为变量。PHP 变量可用于保存值（x=5），也可用于表达式（z=x+y）
变量的名称可以很短（比如 x 和 y），也可以取更具描述性的名称（比如 carname、total_volume）。

以下是PHP变量名的规则：

 - 变量以 $ 符号开头，其后是变量的名称
 - 变量名称必须以字母或下划线开头
 - 变量名称不能以数字开头
 - 变量名称只能包含字母数字字符和下划线（`A-z`、`0-9` 以及 `_`）
 - 变量名称对大小写敏感（$y 与 $Y 是两个不同的变量）

>此外，$this 是一个特殊的变量，它不能被赋值。

我们可以这样给变量赋值：
```php
<?php
	$number = 42;
	$myName = "WangNima";
?>
```

然后这样使用它们：
```php
<?php
	$number = 42;
	$myName = "WangNima";
	echo $number;
	echo $myName;
?>
```
同样很简单是不是？
>时刻牢记：在PHP（和其他很多编程语言）中，单个等号`=`表示的是赋值，即把等号右边的值赋给左边的变量。     
>若要判断两个数是否相等，应当使用双等号`==`(我们后面会讲)


现在来一道练习题，在php中，将自己的名字赋值给一个变量，并利用这个变量输出一句问候。
>提示：使用句点连接字符串

>注：PHP在变量定义中不需要（或不支持）明确的类型定义；变量类型是根据使用该变量的上下文所决定的。
也就是说，如果把一个 string 值赋给变量`$var`，`$var` 就成了一个 `string`。如果又把一个integer 赋给 `$var`，那它就成了一个integer。

##数组
数组是特殊的变量，能够在单独的变量名中同时存储一个或多个值。
在 PHP 中，有三种数组类型：
 * 索引数组 - 带有数字索引的数组
 * 关联数组 - 带有指定键的数组
 * 多维数组 - 包含一个或多个数组的数组       
以下简要介绍一下索引数组和关联数组。


###(普通的)索引数组

我们来考虑这样一种情况：
程序要求记录10个学生的分数，那么这么做固然是可以的：
```php
<?php
	$score1 = 91;
	$score2 = 92;
	$score3 = 93;
	$score4 = 94;
	$score5 = 95;
	$score6 = 96;
	$score7 = 97;
	$score8 = 98;
	$score9 = 99;
	$score10 = 100;
?>
```
然而显而易见的是，这种做法十分的蛋疼。
再想象一下，我们需要列一份购物清单，我们可以为每一件需要买的东西写一张纸（一个变量），然而这并不必要，因为我们可以把所有的东西写在一张纸上。在PHP中，这样的“一张纸”称为数组。

声明一个数组可以这么做：
```php
<?php
	$myarray = array("first","second","third");
?>
```


从这里开始有点小小的不一样了。PHP中，定义数组的时候需要使用`array()`。它告诉php`$myarray`是一个数组，而不是别的什么东西，比如我们之前见到的普通变量。

在上面的例子中，`first`、`second`、`third`都是数组中的元素（他们都是字符串）。数组中的每一项用英文逗号`,`分隔。

数组中的元素也可以是数值或者是别的什么东西：
```php
<?php
	$score = array(22.33,12,450);
?>
```

>因为这里我们输入的是数值，所以不需要加双引号。

定义了数组以后，我们可以这样使用数组中的元素。
```php
<?php
	$myarray = array("first","second","third");
	echo $myarray[1];
?>
```
结果会输出`second`，而不是`first`。这是由于php中，数组的下标（也就是编号）是从0开始计算的。

数组中的元素也是可以改变的，过程类似于给普通变量赋值：
```php
<?php
	$myarray = array(111,222,333);
	echo $myarray[2];  //输出333
	$myarray[2] = 444;
	echo $myarray[2];  //输出444
	/*
	你可能注意到上面的代码最后出现了双斜杠，
	在php中，使用双斜杠可以在代码行末添加注释，
	而像这里一样使用一对斜杠-星号，
	则可以使用多行注释。
	*/
?>
```


###关联数组
>关联数组是使用您分配给数组的指定键的数组。    
通俗的说，索引数组使用数字作为下标来存取数组中的元素，关联数组使得我们可以使用字符串作为数组的下标。

有两种创建关联数组的方法，类似于索引数组：
```php
<?php
	$age = array("Peter"=>"35" , "Ben"=>"37" , "Joe"=>"43");
?>
```
或者
```php
<?php
	$age['Peter'] = "35";
	$age['Ben']   = "37";
	$age['Joe']   = "43";
?>
```
然后就可以在php脚本中使用这些数组了：
```php
<?php
	$age = array("Bill"=>"35" , "Steve"=>"37" , "Peter"=>"43");
	echo "Peter is " . $age["Peter"] . " years old.";
?>
```

##流程控制
目前我们已经见过了字符串和数值，现在我们来学习比较运算符：
 * `>` 大于
 * `<` 小雨
 * `<=` 小于等于
 * `>=` 大于等于
 * `==` 等于
 * `!=` 不等于

###分支结构
>很多情况下，我们需要进行一些判断，为不同的决定执行不同的动作。我们可以在代码中使用条件语句来实现这一点。

在 PHP 中，我们可以使用以下条件语句：
 * if 语句 - 如果指定条件为真，则执行代码
 * if...else 语句 - 如果条件为 真，则执行代码；如果条件为假，则执行另一段代码
 * if...elseif....else 语句 - 选择若干段代码块之一来执行
 * switch 语句 - 语句多个代码块之一来执行

**if 语句用于在指定条件为 true 时执行代码:**
```php
<?php
	if (/*条件*/) {
		// 要执行的代码
	}
?>
```

例如：
```php
<?php
	if ($age >= 18) {
		echo "可以考驾照啦";
	}
?>
```

**if...else语句**
else 延伸了 if 语句，可以在 if 语句中的表达式的值为 FALSE 时执行语句。
```php
<?php
if ($a > $b) {
	echo "a is greater than b";
} else {
	echo "a is NOT greater than b";
}
?>
```

**if...elseif...else 语句**
使用if....elseif...else 语句来选择若干代码块之一来执行。

下例如果当前时间 (HOUR) 小于 10，将输出 "Have a good morning!"。如果当前时间大于等于10且小于 20，则输出 "Have a good day!"。否则将输出 "Have a good night!"：
```php
<?php
$t = 7; //试试改变这个值，观察一下结果会怎样？
if ($t < 10) {
	echo "Have a good morning!";
} elseif ($t < 20) {
	echo "Have a good day!";
} else {
	echo "Have a good night!";
}
?>
```

>其实讲到这里你会发现，PHP的部分语法和C如出一辙，因此这里（包括下面的循环部分）将不会着重讲解语法细节。
建议直接参阅[PHP官方手册](http://php.net/manual/zh/)和[W3School](http://www.w3school.com.cn/php/)的相关文档。

###循环
>和C语言类似，PHP主要有(do)-while和for两种循环  

**while循环**

```php
<?php 
$x=1; 

while($x<=5) {
	echo "这个数字是：$x\n";
	$x++;
} 
?>
```

**for循环**
```php
<?php 
for ($x=0; $x<=10; $x++) {
  echo "数字是：$x <br>";
} 
?>
```

>此外PHP中还有适用于遍历数组的foreach循环，用法可以参考[这里](http://php.net/manual/zh/control-structures.foreach.php)

##函数
>函数是在一个程序中可重复使用的代码片段，可以省下很多复制粘贴的活儿。PHP中有很多内置的函数，下面简单介绍几个来示范函数的使用方法。更多的内置函数使用方法可以参考[官方PHP手册](http://php.net/manual/zh/)

**`strlen()`函数：**

`strlen()`是PHP中用的最多的字符串函数之一。传给这个函数一个字符或者包含字符串的变量作为参数，将返回这个字符串的字符数。例如：
```php
<?php
$len = strlen("blahblah");//在这里随便打点字试试
print $len;
?>
```

>但是`strlen()`并不能很好地处理中文等字符，要计算中文的字数应该使用`mb_strlen()`,用法基本一样。

**`round()`函数：**

`round()`函数用来对数字四舍五入。
```php
<?php
    $r=round(3.1415926);
    echo $r;//输出3

    $r2=round(3.1415926,3);//也可以在第二个参数的位置指定保留几位小数
    echo $r2;//输出3.142
?>
```

##参考资料
1. [PHP官方手册](http://php.net/manual/zh/)

2. [W3School](http://www.w3school.com.cn/index.html)

3. [Codecademy](http://www.codecademy.com/)