---
layout: post
title: tomcat应用启用https
categories: java
---

tomcat应用启用https
=================

# 使用java工具生成keystore 
  
  可以使用%JAVA_HOME%\bin下的keytool来生成keystore，使用如下命令，会生成到~目录下
  
```sh
  %JAVA_HOME%\bin\keytool -genkey -alias tomcat -keyalg RSA
```

# 修改server.xml

  去掉tomcat conf下server.xml的一段注释并修改如下，其中password为上一步生成keystore时填写的。
  
```xml
  <Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
      maxThreads="150" SSLEnabled="true" scheme="https" secure="true" keystorePass="password"
      clientAuth="false" sslProtocol="TLS" />
```

# 修改web.xml

  经过之前的步骤，可同时访问http和https，在自己应用的web.xml下加上以下代码或使用注解的方式来到达自动将访问http转https的目的

```xml
  <security-constraint>
      <web-resource-collection>
      <web-resource-name>securedapp</web-resource-name>
          <url-pattern>/*</url-pattern>
          </web-resource-collection>
      <user-data-constraint>
          <transport-guarantee>CONFIDENTIAL</transport-guarantee>
      </user-data-constraint>
  </security-constraint>
```

# 参考

* [ssl-howto](http://tomcat.apache.org/tomcat-8.0-doc/ssl-howto.html)
* [jsr315](http://download.oracle.com/otndocs/jcp/servlet-3.0-mrel-eval-oth-JSpec/)
