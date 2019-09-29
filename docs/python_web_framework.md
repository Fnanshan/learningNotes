# WSGI是什么？  

WSGI is the Web Server Gateway Interface，就是Web服务网关接口。它是描述web服务器如何与web应用程序通信的规范，以及如何将web应用程序链接在一起来处理一个请求。

Django 的主要部署平台是 WSGI，它是 Web 服务器和 Web 应用的 Python 标准。

#python manage.py runserver  
启动的是 Django 自带的用于开发的简易服务器，它是一个用纯 Python 写的轻量级的 Web 服务器。

**千万不要**将这个服务器用于和生产环境相关的任何地方。这个服务器只是为了开发而设计的。
python web的服务器不要使用Django，可以用Apache HTTP Server或者Nginx等。

# tomcat 与 nginx，apache的区别是什么？  
简单的说，Tomcat是运行Java程序的容器。nginx和apache是HTTP Server。绝大多数编程语言所包含的类库中也都实现了简单的HTTP服务器方便开发者使用：

* HttpServer (Java HTTP Server )
* Python SimpleHTTPServer

与Apache HTTP Server相比，Tomcat能够动态的生成资源并返回到客户端。

Apache HTTP Server和Nginx本身不支持生成动态页面，但它们可以通过其他模块来支持（例如通过Shell、PHP、Python脚本程序来动态生成内容）。

如果想要使用Java程序来动态生成资源内容，使用这一类HTTP服务器很难做到。Java Servlet技术以及衍生的Java Server Pages技术可以让Java程序也具有处理HTTP请求并且返回内容（由程序动态控制）的能力，Tomcat正是支持运行Servlet/JSP应用程序的容器（Container）
作者：David

链接：https://www.zhihu.com/question/32212996/answer/87524617

来源：知乎

著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

**学习django过程中，在生产环境可以了解Apache HTTP Server的使用，但是写代码的时候还是以django自带的HTTP Server为主。**

# 如何安装 Django  
## 安装 Apache 和 mod_wsgi  
如果要在生产站点上使用 Django，请将 Apache 与 mod_wsgi 一起使用。  

### mod_wsgi是什么？  
mod wsgi包实现了一个简单易用的Apache模块，它可以承载任何支持Python wsgi规范的Python web应用程序。根据您的需求，可以用两种不同的方式安装包。手动配置和自动配置。  

# 模型和数据库  
每一个模型都映射一张数据库表。  
