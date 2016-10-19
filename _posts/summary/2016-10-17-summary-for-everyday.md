---
layout: post
title: Summary
abstract: 每天把当日的收获记下来，巩固基础知识，学习最新技术
categories: summary
tags: [summary, js]
hasTag: true
comments: true
---

#  日积月累

## 5.5
* dom.offsetTop  得到dom相对于offsetParent的top
* git diff   比较workspace与暂存区的区别
* git diff --cached   比较暂存区与上次commit的区别
* git diff HEAD      显示工作区与上次commit的区别
* git stash  保持工作区中的改动
* git stash pop  还原工作区中的改动
* 查看文件中某几行的提交记录
  git log -L 12,15:debug.js
* 将某文件回滚到master 
  先到maser上查看最近的提交id
  git checkout 1bdacda42a658f6481b93e3cfc5415fa1b1867c7 -- debug.js
* 撤销对文件的修改   git checkout -- 文件名
* git reset --hard HEAD^(或者提交id)
  重置上一次提交前所有的改动
* git commit --amend -m "commit message"  修改上一次提交
* git blame 文件名  查看文件的每一行是哪个提交修改的
* git log -p 文件名  查看文件的提交记录

## 5.6
* chmod  设置文件权限  wrx  例如chmod ugo+wrx ./xxx, 其中w是写权限（4），r是读权限（2），x是执行权限（1）
* tail -f 文件名
* more  less

## 5.9
* 解决ios下  fixed定位时输入框乱跳的问题  采用absolute定位
    	
```js
if(sniff.ios){
	$input.on('blur', function(){
		setTimeout(function(){
			//如果没有弹出键盘，重绘一下弹出页
			if(!$('input').is(':focus')){
				$container.css({
					height: (window.screen.availHeight + 'px'),
					top:(document.body.scrollTop + 'px')
				});
			}
		}, 500);
	});
}
```
* 用div加背景替代img标签可以方便的保证图片的比例，如果图片过大自动进行截取，不会出现比例失调的现象
* export = PATH=/usr/xxx:$PATH 可以修改linux的path，如果要永久生效，需修改/etc/profile，将代码加到该文件下，每次开机系统会自动执行该文件
* flip.js
* timeline

## 5.18
* 使div横向排列：white-space: nowrap
* qunar app schema: schema://hy?type=browser&url=xxxx

## 7.13
* dom.offsetLeft
* 删除分支   git branch -d 分支名
* async  script标签上的async属性代表当script标签加载好后就会执行
* defer  代表当页面完成解析时script才会执行
* 既没有async也没有defer  script标签会阻塞页面的解析

## 7.18
* window.onload  页面上所有的资源（包括图片）加载好后，才触发window.onload事件
* find shell
  find / -name fekit   查找fekit
* 数组方法 some 当返回true时终止遍历

## 7.19
* 浏览器缓存的规则
对于浏览器端的缓存来讲，这些规则是在HTTP协议头和HTML页面的Meta标签中定义的。他们分别从新鲜度和校验值两个维度来规定浏览器是否可以直接使用缓存中的副本，还是需要去源服务器获取更新的版本。 新鲜度（过期机制）：也就是缓存副本有效期。一个缓存副本必须满足以下条件，浏览器会认为它是有效的，足够新的：
	1.	含有完整的过期时间控制头信息（HTTP协议报头），并且仍在有效期内；
	2.	浏览器已经使用过这个缓存副本，并且在一个会话中已经检查过新鲜度；
满足以上两个情况的一种，浏览器会直接从缓存中获取副本并渲染。
校验值（验证机制）：服务器返回资源的时候有时在控制头信息带上这个资源的实体标签Etag（Entity Tag），它可以用来作为浏览器再次请求过程的校验标识。如过发现校验标识不匹配，说明资源已经被修改或过期，浏览器需求重新获取资源内容。
* 浏览器缓存控制
Cache-Control与Expires
Cache-Control与Expires的作用一致，都是指明当前资源的有效期，控制浏览器是否直接从浏览器缓存取数据还是重新发请求到服务器取数据。只不过Cache-Control的选择更多，设置更细致，如果同时设置的话，其优先级高于Expires。
Last-Modified/ETag与Cache-Control/Expires
配置Last-Modified/ETag的情况下，浏览器再次访问统一URI的资源，还是会发送请求到服务器询问文件是否已经修改，如果没有，服务器会只发送一个304回给浏览器，告诉浏览器直接从自己本地的缓存取数据；如果修改过那就整个数据重新发给浏览器；
Cache-Control/Expires则不同，如果检测到本地的缓存还是有效的时间范围内，浏览器直接使用本地副本，不会发送任何请求。两者一起使用时，Cache-Control/Expires的优先级要高于Last-Modified/ETag。即当本地副本根据Cache-Control/Expires发现还在有效期内时，则不会再次发送请求去服务器询问修改时间（Last-Modified）或实体标识（Etag）了。
一般情况下，使用Cache-Control/Expires会配合Last-Modified/ETag一起使用，因为即使服务器设置缓存时间, 当用户点击“刷新”按钮时，浏览器会忽略缓存继续向服务器发送请求，这时Last-Modified/ETag将能够很好利用304，从而减少响应开销。
Last-Modified与ETag
你可能会觉得使用Last-Modified已经足以让浏览器知道本地的缓存副本是否足够新，为什么还需要Etag（实体标识）呢？HTTP1.1中Etag的出现主要是为了解决几个Last-Modified比较难解决的问题：
	1.	Last-Modified标注的最后修改只能精确到秒级，如果某些文件在1秒钟以内，被修改多次的话，它将不能准确标注文件的新鲜度
	2.	如果某些文件会被定期生成，当有时内容并没有任何变化，但Last-Modified却改变了，导致文件没法使用缓存
	3.	有可能存在服务器没有准确获取文件修改时间，或者与代理服务器时间不一致等情形
Etag是服务器自动生成或者由开发者生成的对应资源在服务器端的唯一标识符，能够更加准确的控制缓存。Last-Modified与ETag是可以一起使用的，服务器会优先验证ETag，一致的情况下，才会继续比对Last-Modified，最后才决定是否返回304。
* 哪些请求不被缓存
无法被浏览器缓存的请求：
	1.	HTTP信息头中包含Cache-Control:no-cache，pragma:no-cache，或Cache-Control:max-age=0等告诉浏览器不用缓存的请求
	2.	需要根据Cookie，认证信息等决定输入内容的动态请求是不能被缓存的
	3.	经过HTTPS安全加密的请求（有人也经过测试发现，ie其实在头部加入Cache-Control：max-age信息，firefox在头部加入Cache-Control:Public之后，能够对HTTPS的资源进行缓存，参考《HTTPS的七个误解》）
	4.	POST请求无法被缓存
	5.	HTTP响应头中不包含Last-Modified/Etag，也不包含Cache-Control/Expires的请求无法被缓存
	
##  7.20
* word-break: 当行尾放不下一个单词时决定单词内部该怎么摆放
  break-all: 挤不下的换一行显示
  keep-all: 挤不下的另起一行展示
* word-wrap: 当行尾放不下时决定单词内是否允许换行
  normal: 单词太长，换行显示，再超过一行就溢出显示
  break-word: 当单词太长，先尝试换行，换行后还展示不下，单词内可以换行
* write-space: 处理空格，浏览器默认会压缩空格
  pre: 保留所有的空格和回车
  pre-wrap: 保留所有的空格和回车，但允许换行
  pre-line: 会合并空格，允许折行
  
## 7.24
* 伪类和伪元素
css引入伪类和伪元素概念是为了格式化文档树以外的信息。也就是说，伪类和伪元素是用来修饰不在文档树中的部分，比如，一句话中的第一个字母，或者是列表中的第一个元素。
伪类用于当已有元素处于的某个状态时，为其添加对应的样式，这个状态是根据用户行为而动态变化的。比如说，当用户悬停在指定的元素时，我们可以通过:hover来描述这个元素的状态。虽然它和普通的css类相似，可以为已有的元素添加样式，但是它只有处于dom树无法描述的状态下才能为元素添加样式，所以将其称为伪类。
伪元素用于创建一些不在文档树中的元素，并为其添加样式。比如说，我们可以通过:before来在一个元素前增加一些文本，并为这些文本添加样式。虽然用户可以看到这些文本，但是这些文本实际上不在文档树中。
* 居中的css
  
```
  #container2 {
      position: relative;
      width: 400px;
      height: 400px;
      background-color: #f00;
  }

  #box6 {
      width: 50%;
      height: 50%;
      overflow: auto;
      margin: auto;
      position: absolute;
      top: 0;
      left: 0;
      bottom: 0;
      right: 0;
      background-color: #0f0;
  }
```

```
  #container2 {
 		display: flex;
 		-webkit-display: flex;
 		justify-content: center;
		 align-items: center;
		 width: 400px;
		 height: 400px;
		 background-color: #f00;
  }

  #box6 {
		 width: 50%;
		 height: 50%;
		 background-color: #0f0;
  }
```
  
```
	#demo {
	  	height: 100px;
	  	text-align: center;
	}
	
	#demo:after {
	  display: inline-block;
	  width: 0;
	  height: 100%;
	  vertical-align: middle;
	  content: '';
	}
	
	#demo p {
	  display: inline-block;
	  vertical-ali
	}
```
* viewport
早期苹果定义了一个layout-viewport布局视口，而这个视口的分辨率接近pc显示器的分辨率，苹果定义的是980px
以iphone为例，如果没有设置viewport，viewport-layout的宽度就是980px，如果设置100*100px的矩形区域，看起来就是屏幕的100/980，如果设置了viewport width=device-width，iphone4的view-layout的宽度就是320px，如果设置100*100的矩形区域，看起来就是屏幕的100/320
visual-layout: 手持设备物理屏幕的可视区域
以iphone4s为例，会在320*480的visual-viewport中创建一个宽980px的layout-viewport，

## 08.01
* 前端优化： 减少dom的渲染，减少图片的加载，精简js
* shell: 查看端口号被哪个进程占用  lsof -i:80   杀掉某个进程  kill -pid

## 08.17
* javascript是值传递的
例子1

```
var me = {					// 1
	'partOf' : 'A Team'
}; 

function myTeam(me) {		// 2

	me = {					// 3
		'belongsTo' : 'A Group'
	}; 
} 	

myTeam(me);		
console.log(me);	
```
例子2

```
var me = {					// 1
	'partOf' : 'A Team'
}; 

function myGroup(me) { 		// 2
	me.partOf = 'A Group';  // 3
} 

myGroup(me);
console.log(me);	
```
## 08.18
* chrome dev调试：cmd+o 查找文件  cmd+shift+o 查找函数
* promise的catch会接收到reject后传递的参数
* shell相关：
  sudo service qunar_package_mobile_abroadshop start
  lsof -i tcp:9001
  ps -ef | grep forever
  
##  08.24 
* 安装nginx
```brew install nginx --with-http_geoip_module
```
* Nginx启动关闭命令：
```
#测试配置是否有语法错误
nginx -t
#打开 nginx
sudo nginx
#重新加载配置|重启|停止|退出 nginx
nginx -s reload|reopen|stop|quit
#也可以使用Mac的launchctl来启动|停止
launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.nginx.plist
launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.nginx.plist
```
* Nginx开机启动
```ln -sfv /usr/local/opt/nginx/*.plist ~/Library/LaunchAgents
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.nginx.plist
Nginx监听80端口需要root权限执行，因此：
sudo chown root:wheel /usr/local/Cellar/nginx/1.6.0_1/bin/nginx
sudo chmod u+s /usr/local/Cellar/nginx/1.6.0_1/bin/nginx
```
* 配置nginx.conf
* 创建需要用到的目录：


```mkdir -p /usr/local/var/logs/nginx
mkdir -p /usr/local/etc/nginx/sites-available
mkdir -p /usr/local/etc/nginx/sites-enabled
mkdir -p /usr/local/etc/nginx/conf.d
mkdir -p /usr/local/etc/nginx/ssl
sudo mkdir -p /var/www
sudo chown :staff /var/www
sudo chmod 775 /var/www
```
# 09.02
* nginx地址：/usr/local/etc/nginx/
* node起服务：
  node ./bin/start -l ../logs/
  sudo service qunar_package_mobile_abroadshop stop
  sudo service qunar_package_mobile_abroadshop start
  
# 09.21
* xcode build app
  Pods Debug 加BETA_BUILD=1
  Vacation下的Pod Debug 加BETA_BUILD=1 
  
# 09.22
* chrome中搜索方法名：command + alt + f
* chrome中搜索文件名: command + o
* 查看占用端口号的进程：sudo lsof -n -i4TCP:8081 | grep LISTEN
* 杀死进程  kill -9 nodeid
* which react-native

# 09.28
* shell: find . -name "*ios*" -print -maxdepth 1
  find . -type d -print -maxdepth 1  查找类型为文件夹的
  find . \( -name "*index*" -prune \) -o \( -name "*ios*" \) -maxdepth 1 -print 
  cat index.ios.js | grep "firstProject"
  
# 10.14
* 如果浏览器和服务器都支持的情况下，可以使用压缩减小响应的大小，浏览器可以使用Accept-Encoding来告诉服务器支持的压缩类型，服务器可以使用Content-Encoding来声明使用了那种压缩方式
* 条件GET请求：如果浏览器保存了一份资源副本，但并不确认它是否有效，就会发送一个条件GET请求。浏览器通过http头的If-Modified-Since字段来告诉服务器副本的最后修改时间是什么，服务器通过Last-Modified-Since字段来告诉浏览器副本是否过期
* Vary: 代理会根据不同情况为各种情况都缓存一份副本  如 Vary:Accept-Encoding
* 性能优化
  减少http请求、使用内容分发网络



	
	






  


