---
layout : post
title : web server
---
```
<server port="8005" shutdown="SHUTDOWN">  
  <service name="Catalina">  

      <engine defaulthost="localhost" name="Catalina">  

         <host appbase="webapps" autodeploy="true" name="localhost" unpackwars="true"></host>  
         <host appbase="ramki_webapps" autodeploy="true" name="www.ramki.com" unpackwars="true"></host>  
         <host appbase="krishnan_webapps" autodeploy="true" name="www.krishnan.com" unpackwars="true"></host>  
         <host appbase="blog_webapps" autodeploy="true" name="www.blog.ramki.com" unpackwars="true"></host>  


    </engine>  
  </service>  
</server>  


<server>
    className   :   server实现类
    address     :   优雅的关掉tomcat
    port        :   优雅的关掉tomcat
    shutdown    :   优雅的关掉tomcat


<Service>
    className   :   实现类
    name        :   名字，用于

<Connector>
    allowTrace      :   enable or disable the TRACE HTTP method
    asyncTimeout    :   timeout for asynchronous requests in milliseconds
    enableLookups   :   enable DNS lookups are disabled
    maxHeaderCount  :   The maximum number of headers in a request,If not specified, a default of 100 is used.
    maxParameterCount   :   The maximum number of parameter and value pairs
    maxPostSize     :   
    maxSavePostSize :
    parseBodyMethods:
    port            :
    protocol        :   选择connector的实现。
    proxyName       :   
    proxyPort       :
    redirectPort    :   针对ssl重定向
    scheme          :
    secure          :
    URIEncoding     :
    useBodyEncodingForURI   :
    useIPVHosts     :   基于域名的虚拟主机还是基于ip的虚拟主机
    xpoweredBy      :

<Engine>
    Exactly one Engine element MUST be nested inside a Service element, following all of the corresponding Connector elements associated with this Service.
    与顺序有关，且只有一个
    backgroundProcessorDelay    :
    className   :   实现类
    defaultHost :   必须是Host中指定的一个   
    jvmRoute    :   
    name        :   记日志，muti service中唯一性表示
```
