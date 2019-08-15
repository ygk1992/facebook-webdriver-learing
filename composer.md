#facebook/webdriver

①、facebook/webdriver是一个PHP客户端连接selenium webdriver。
可以在composer的官方镜像上通过composer下载这个包。


##一、安装composer包管理器

怎么下载呢？可以通过composer去下载这个包

①、首先确定自己安装了composer的PHP包管理工具。

在Windows上可以一种方法是取composer官网中去下载二进制安装包。

安装很简单，傻瓜式安装，下一步，下一步即可。

注意composer是一个PHP包管理工具。所以须有php解释器。
在安装的时候，composer会自动找PHP解释器（前提是把php解释器放在环境变量中）。

安装完后如果在cmd中输入`composer --version`就可以看到当前安装的composer版本啦。

如果安装的时候，提示composer不是一个可执行文件，需要把composer.bat放到Windows环境变量中。

在*unix系统安装composer可以使用

    curl -sS https://getcomposer.org/installer | php

安装库的话使用命令：
    php composer.phar require facebook/webdriver


由于composer安装包时使用的镜像是在国外，可能下载包会速度比较慢，
可以指定一下composer的镜像配置，指定镜像有两种方式：
①是全局composer配置指定镜像。这样所有项目都会使用这个镜像（推荐这种配置）。

    composer config -g repo.packagist composer https://packagist.phpcomposer.com

②是在项目中的composer.json中配置镜像。
在composer.json中指定镜像配置。

    "repositories": {
	    "packagist": {
	        "type": "composer",
	        "url": "https://packagist.phpcomposer.com"
	    }
    }

##二、在项目中使用facebook/webdriver包

到项目目录下，执行

    composer require facebook/webdriver

最近的正式版：需要依赖：

1. php:^5.6 || ~7.0
2. symfony/process:^2.8 || ^3.1 || ^4.0
3. ext-curl：*（无版本要求）
4. ext-zip：*(无版本要求)
5. ext-mbstring:*(mbstring无版本要求)
6. ext-json:*(json无版本要求)

 ###描述下facebook/webdriver

它是什么？

php-webdriver是一个PHP显示的连接selenium webdriver的库。


它能干嘛呢？

它可以控制你通过PHP控制浏览器。

我们知道两个软件要想交流，必须规定一种说话方式。
要不一个软件说话，对方不能理解，这不是我们想要的。
所以出现了一种标准。这个标准在计算机网络就是协议（protocol）。
php-webdriber和selenium webdriver通信使用的协议是什么呢？
它们之间通信有两种协议。一种是jsonWireProtocol。两位一种协议是W3C WebDriver协议。这个协议还没有在php-webdriver中实现。或许会在以后的Facebook/webdriver库中实现这个协议。

##开始使用这个包

①、首先需要启动selenium server。

启动的话，我们得安装它吧？
安装它的话。我们必须得有这个安装包啊？
我们去哪儿获取这个安装呢？
①、去官网下载：

    http://selenium-release.storage.googleapis.com/index.html

下载完成后，就是jar包。jar包是什么包呢。jar包就是个使用jdk打的一个包。所以需要依赖java环境。需要安装jdk。安装完jdk后。可以使用如下命令来启动selenium-server

    java -jar F:\chromedriver_win32\selenium-server-standalone-2.46.0.jar ^
    -timeout=20 ^
    -browserTimeout=60 ^
    -Dwebdriver.chrome.driver=F:\chromedriver_win32\chromedriver.exe


通过上面的命令就启动了。启动完成后。会有一个session地址。
启动后默认监听4444端口。启动会有个说明remoting webdriver should

connect to http://127.0.0.1:4444/wd/hub


    $host = "http://127.0.0.1:4444/wd/hub";


#####通过PHP启动Chrome浏览器。

    $driver = RemoteWebDriver::create($host, DesiredCapabilities::chrome);

####通过PHP启动火狐浏览器

请确保安装了最新的火狐浏览器和Geckordriver。

因为火狐浏览器仅仅支持W3C 	WebDriver协议（它还在没有被php-webdriver实现），而且需要安装Selenium Server3.5.0-4.8-2
你可以使用下面的命令来启动它。

    java -jar selenium-server--standalone-3.8.1.jar -enablePassThrough false

现在你可以使用下面的PHP脚本来启动火狐浏览器了。

     $driver = RemoteWebDriber::create($host, DesiredCapabilities::firefox());

###使用php-webdriver实现自定义所需的功能

可以使用下面的命令：

    $desired_capabilities = DesiredCapabilities::firefox();
    $desire_capabilities->setCapability("acceptSslCerts", false);
    $driber = RemoteDriver::create($host, $desired_capabilities);

注意：更多使用去https:://github.com.SeleniumHQ/selenium/wiki/DesiredCapabilities。


####集成测试框架

如果你想把php-webdriver集成到你的集成测试框架中去。
已经有一些开源的工具了。

①、Steward 集成php-webdriver到PHPUnit，并且提供了并行测试。
②、Codeception
③、你可以检出blogpost+demo project。

blogpost链接地址：
    http://codeception.com/11-12-2013/working-with-phpunit-and-selenium-webdriver.html
demo project：
    https://github.com/DavertMik/php-webdriver-demo


#####遇到问题去哪儿去找问题的解决方案

①、可以去stack Overflow。
②、可以去Facebook社区。
③、通过GitHub。如果你有问题获取bug可以直接去
    https://github.com/facebook/php-webdriver/issues/new提议



