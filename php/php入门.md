PHP入门教程
=========================
>PHP 是一种创建动态交互性站点的强有力的服务器端脚本语言，本文档将会介绍一些基础的PHP知识。学习完成本教程后，将获得建立简单动态网站的能力。本文档需要一点点HTML的基础知识，可以先参考这篇[前端入门文档](https://github.com/Njupt-Sast-Network/document/blob/master/fem/fem入门那点小事/home.md)。

###简介
学习PHP之前，我们首先要了解web前端和后端的关系 
<!-- 
待填坑，可以讲讲从静态网页发展到动态网页，数据的持久储存blahblah
 -->
PHP的全称为：PHP：Hypertext Preprocessor，即“PHP：超文本预处理器”，是一种开源的通用计算机脚本语言，尤其适用于网络开发并可嵌入HTML中使用。易于学习，入门简单是其特点之一。

客户端在向web服务器请求php页面的时候，服务器上的php解析器通过运行php脚本中的php代码来生成纯html页面，并将其传输给客户端。最终客户端收到的html页面中将不包含php代码。若需要在自己的电脑上进行php开发，就需要在电脑上安装php解析器。

通常，类似于[XAMPP](https://www.apachefriends.org/zh_cn/index.html)这样的建站集成包会整合web开发所需的软件（Apache网页服务器+PHP+MySQL数据库），因此在Windows下只需安装XAMPP即可获得能够运行php的环境。Mac系统和Linux系统<!-- 待填坑 -->

###基本语法
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

###Getting Started

>注：以下假定使用的是windows系统，并以默认设置安装了XAMPP。其他建站包和操作系统请自行参考其他文档。

首先我们在web根目录（通常是C:\xmapp\htdocs）下新建一个空白文本文档，并命名为index.php

>如果新安装了XAMPP,htdocs会包含一些附带的实例页面，请先将这些页面删除或者移到其他地方。此外Windows默认会隐藏文件后缀名，注意不要创建为index.php.txt这样的文件

使用文本编辑器（推荐[Sublime Text](http://www.sublimetext.com/)）打开这个文件，并如下输入：

```php
<?php
	echo "Hello,World";
?>
```

和C语言类似，每个php语句以分号`;`结尾。

echo函数会输出字符串，php中字符串以一对双引号包围。

保存这个文件，打开XAMPP的控制面板并启动Apache网页服务器（它会调用php解析引擎），打开浏览器并在地址栏输入`127.0.0.1`，回车。

>注：`127.0.0.1`这个被称为“本地环回”的特殊的IP地址会指向本机上的服务
>如果在XAMPP中无法启动Apache，并且看到了类似于这样的提示：
>21:48:34  [Apache] 	Problem detected!
>21:48:34  [Apache] 	Port 443 in use by ""C:\Program Files (x86)\VMware\VMware Workstation\vmware-hostd.exe" -u "C:\ProgramData\VMware\hostd\config.xml"" with PID 1956!
>21:48:34  [Apache] 	Apache WILL NOT start without the configured ports free!
>21:48:34  [Apache] 	You need to uninstall/disable/reconfigure the blocking application
>21:48:34  [Apache] 	or reconfigure Apache and the Control Panel to listen on a different port
>
>那么说明VMWare占用了Apache使用的443端口，请前往VMWare的首选项->共享虚拟机中禁用共享，或者改用其他空闲端口。

如果一切正常的话，应该能在浏览器中看到我们~~喜闻乐见~~的Hello,World了。
![喜闻乐见的Hello,World](https://raw.githubusercontent.com/Njupt-Sast-Network/document/master/php/pic/gettingstarted1.png)

如果看到了`Hello,World`，那么恭喜你，你已经成功地写出了第一个php页面。