在在线状态下更具清单配置文件(cache.manifest)下载js文件、css文件和图片等资源存储在客户端本地，
在离线的状态时，访问存资源文件，呈现web页面。

html5提供了里此案应用的特性，但是具体怎么去实现，由web开发者自己决定。

离线web应用的核心是缓存清单文件(cache.manifest),其中包含了在线状态下web应用有可能访问的资源

需要将<html>标签的manifest属性指向缓存文件。

	<!DOCTYPE HTML>
	<html manifest = "cache.manifest">
	...
	</html>

**注：**

如果web应用包含多了页面，如果这些页面都需要使用离线访问功能，需要在每个页面社会manifest属性。


关于cache.manifest文件的格式：
1、每个缓存清单文件通常都已如下两行开头，其中第一行是必须的，第二行的注释形式的版本号可以在必要时更新。
应为在某些情况下，css文件或者js文件有改动，但是其资源的url并没有变化，这样如果没有其他的标识，清单文件
并不会变化。引入注释形式的版本号正式处于这种考虑。

	CACHE MANIFEST
	#v0.15
2、包含三个部分：CACHE段、NETWORK段、FALLBACK段
CACHE声明的资源在在线状态会被下载下来，缓存到本地，在离线状态下使用。
NETWORK声明的资源不会被缓存，
FALLBACK声明的资源表示为那些由于某些原因无法被缓存或者缓存失败的资源指定资源。


1)浏览器通过普通恩地HTTP予以来检测缓存清单文件是否过期，web服务器会在响应头中包含描述该文件过期时间的
信息，通过设置(Expires或者Cache-Control)，这种方式的缓存不是为离线web应用专门提供的，
而是所欲html页面、样式文件、脚本文件、图片及其他web资源都会使用这种方式。

2)缓存文件也有可能存在过期，如果缓存文件过期，那么浏览器会“询问”服务器是否改文件有改动。有的话就下载
最新的资源清单文件，如何实现呢？

其实实现额方式跟普通的文件一样，浏览器会想服务器发送一个http请求，该请求中包含缓存文件最后一次修改的时间
（此时间是上一次浏览器下载缓存文件时，服务器通过http响应头告诉浏览器的），然后服务器会获取服务端该缓存文件最后一次修改的时间
，将两者时间进行对比，如果一致，则表示资源没有修改，简单的返回304状态码，并重新告诉浏览器该资源最后一次修改的时间。
如果不一致，表示该资源在服务端有修改。

所有的web资源都会这样处理，应为缓存清单文件也是一个普通的web资源文件。


正式由于缓存文件和普通原件一样存在资源有效期的概念，如果服务端在资源有效期内修改了资源清单文件。
但是浏览器的资源清单文件还在有效期内，即使刷新页面，浏览器也不会向服务器重写请求缓存清单文件。带来调试上的不便利。

因此，有改变缓存清单文件的http头消息缓存机制。


一个cache.manifest文件实例：

	CACHE MANIFEST
	#v0.15

	CACHE:

	/components/css/bootstrap.min.css
	/components/css/bootstrap-responsive.min.css
	/components/css/font-awesome.css
	/components/css/adminia.css
	/components/css/adminia-responsive.css
	/components/css/pages/dashboard.css
	/components/img/headshot.png
	/components/img/body-bg.png
	/components/font/fontawesome-webfont.woff
	/components/font/fontawesome-webfont.ttf
	/css/dropzone.css
	/js/dropzone.min.js
	/components/js/bootstrap.js
	/components/js/jquery-1.7.2.min.js

	NETWORK:
	/img/spritemap.png

	FALLBACK:
