## HTTP报文格式

HTTP报文分为请求报文和响应报文两种，每种报文必须按照特有格式生成，才能被浏览器端识别。其中，浏览器端向服务器发送的为请求报文，服务器处理后返回给浏览器端的为响应报文

​			

### 请求报文

HTTP请求报文有请求行(request line)、请求头部(header)、空行和请求数据四个部分组成。

其中，请求分为两种，GET和POST，具体的：

- GET

   1  GET /562f25980001b1b106000338.jpg HTTP/1.1
   2  Host:img.mukewang.com
   3  User-Agent:Mozilla/5.0 (Windows NT 10.0; WOW64)
   4  AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.106 Safari/537.36
   5  Accept:image/webp,image/*,*/*;q=0.8
   6  Referer:http://www.imooc.com/
   7  Accept-Encoding:gzip, deflate, sdch
   8  Accept-Language:zh-CN,zh;q=0.8
   9  空行
  10  请求数据为空

  ​		

- POST

  1  POST / HTTP1.1
  2  Host:www.wrox.com
  3  User-Agent:Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 2.0.50727; .NET CLR 3.0.04506.648; .NET CLR 3.5.21022)
  4  Content-Type:application/x-www-form-urlencoded
  5  Content-Length:40
  6  Connection: Keep-Alive
  7  空行
  8  name=Professional%20Ajax&publisher=Wiley

  ​		

- **请求行**，用来说明请求类型,要访问的资源以及所使用的HTTP版本。
  GET说明请求类型为GET，/562f25980001b1b106000338.jpg(URL)为要访问的资源，该行的最后一部分说明使用的是HTTP1.1版本。

- **请求头部**，紧接着请求行（即第一行）之后的部分，用来说明服务器要使用的附加信息。

- - HOST，给出请求资源所在服务器的域名。
  - User-Agent，HTTP客户端程序的信息，该信息由你发出请求使用的浏览器来定义,并且在每个请求中自动发送等。
  - Accept，说明用户代理可处理的媒体类型。
  - Accept-Encoding，说明用户代理支持的内容编码。
  - Accept-Language，说明用户代理能够处理的自然语言集。
  - Content-Type，说明实现主体的媒体类型。
  - Content-Length，说明实现主体的大小。
  - Connection，连接管理，可以是Keep-Alive或close。

- **空行**，请求头部后面的空行是必须的即使第四部分的请求数据为空，也必须有空行。

- **请求数据**也叫主体，可以添加任意的其他数据。

  ​	

GET和POST的区别

- 最直观的区别就是GET把参数包含在URL中，POST通过request body传递参数。
- GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留。
- GET请求在URL中传送的参数是有长度限制。（大多数）浏览器通常都会限制url长度在2K个字节，而（大多数）服务器最多处理64K大小的url。
- GET产生一个TCP数据包；POST产生两个TCP数据包。对于GET方式的请求，浏览器会把http header和data一并发送出去，服务器响应200（返回数据）；而对于POST，浏览器先发送header，服务器响应100（指示信息—表示请求已接收，继续处理）continue，浏览器再发送data，服务器响应200 ok（返回数据）。





### 响应报文

HTTP响应也由四个部分组成，分别是：状态行、消息报头、空行和响应正文。

 1	HTTP/1.1 200 OK
 2	Date: Fri, 22 May 2009 06:07:21 GMT
 3	Content-Type: text/html; charset=UTF-8
 4	空行
 5	<html>
 6  	 <head></head>
 7   	<body>
 8      	<!--body goes here-->
 9 	  </body>
10	</html>

​			

- 状态行，由HTTP协议版本号， 状态码， 状态消息 三部分组成。
  第一行为状态行，（HTTP/1.1）表明HTTP版本为1.1版本，状态码为200，状态消息为OK。

- 消息报头，用来说明客户端要使用的一些附加信息。
  第二行和第三行为消息报头，Date:生成响应的日期和时间；Content-Type:指定了MIME类型的HTML(text/html),编码类型是UTF-8。

- 空行，消息报头后面的空行是必须的。

- 响应正文，服务器返回给客户端的文本信息。空行后面的html部分为响应正文。

  ​		

## HTTP状态码

HTTP有5种类型的状态码，具体的：

- 1xx：指示信息--表示请求已接收，继续处理。

- 2xx：成功--表示请求正常处理完毕。

- - 200 OK：客户端请求被正常处理。
  - 206 Partial content：客户端进行了范围请求。

- 3xx：重定向--要完成请求必须进行更进一步的操作。

- - 301 Moved Permanently：永久重定向，该资源已被永久移动到新位置，将来任何对该资源的访问都要使用本响应返回的若干个URI之一。
  - 302 Found：临时重定向，请求的资源现在临时从不同的URI中获得。

- 4xx：客户端错误--请求有语法错误，服务器无法处理请求。

- - 400 Bad Request：请求报文存在语法错误。
  - 403 Forbidden：请求被服务器拒绝。
  - 404 Not Found：请求不存在，服务器上找不到请求的资源。

- 5xx：服务器端错误--服务器处理请求出错。

- - 500 Internal Server Error：服务器在执行请求时出现错误。
  - ​	

## 有限状态机

有限状态机，是一种抽象的理论模型，它能够把有限个变量描述的状态变化过程，以可构造可验证的方式呈现出来。比如，封闭的有向图。

有限状态机可以通过if-else,switch-case和函数指针来实现，从软件工程的角度看，主要是为了封装逻辑。

带有状态转移的有限状态机示例代码。

 1	STATE_MACHINE(){
 2 	 State cur_State = type_A;
 3  	while(cur_State != type_C){
 4  	  Package _pack = getNewPackage();
 5    	switch(){
 6      	case type_A:
 7        	cur_State = type_B;
 9      	  break;
10     	 case type_B:
11       	 process_pkg_state_B(_pack);
12        	cur_State = type_C;
13        	break;
14  	  }
15 	 }
16	}

该状态机包含三种状态：type_A，type_B和type_C。其中，type_A是初始状态，type_C是结束状态。

状态机的当前状态记录在cur_State变量中，逻辑处理时，状态机先通过getNewPackage获取数据包，然后根据当前状态对数据进行处理，处理完后，状态机通过改变cur_State完成状态转移。

有限状态机一种逻辑单元内部的一种高效编程方法，在服务器编程中，服务器可以根据不同状态或者消息类型进行相应的处理逻辑，使得程序逻辑清晰易懂。