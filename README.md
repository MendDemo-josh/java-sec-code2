# Java Security Code

## 介绍

该项目也可以叫做Java Vulnerability Code(Java漏洞代码)。

每个漏洞类型代码默认存在安全漏洞（除非本身不存在漏洞），相关修复代码在注释里。具体可查看每个漏洞代码和注释。

## 漏洞代码

- [XXE](https://github.com/JoyChou93/java-sec-code/blob/master/src/main/java/org/joychou/controller/XXE.java)
- [SSRF](https://github.com/JoyChou93/java-sec-code/blob/master/src/main/java/org/joychou/controller/SSRF.java)
- [URL重定向](https://github.com/JoyChou93/java-sec-code/blob/master/src/main/java/org/joychou/controller/URLRedirect.java)
- [IP伪造](https://github.com/JoyChou93/java-sec-code/blob/master/src/main/java/org/joychou/controller/IPForge.java)
- [XSS](https://github.com/JoyChou93/java-sec-code/blob/master/src/main/java/org/joychou/controller/XSS.java)
- [CRLF注入](https://github.com/JoyChou93/java-sec-code/blob/master/src/main/java/org/joychou/controller/CRLFInjection.java)
- [远程命令执行](https://github.com/JoyChou93/java-sec-code/blob/master/src/main/java/org/joychou/controller/Rce.java)
- [反序列化](https://github.com/JoyChou93/java-sec-code/blob/master/src/main/java/org/joychou/controller/Deserialize.java)

## 如何运行


### Tomcat

1. 生成war包 `mvn clean package`
2. 将target目录的war包，cp到Tomcat的webapps目录
3. 重启Tomcat应用


```
http://localhost:8080/java-sec-code-1.0.0/rce/exec?cmd=whoami
```
 
返回

``` 
Viarus
```

### IDEA

如果想在IDEA中直接运行，需要在IDEA中添加Tomcat配置，步骤如下：

```
Run -> Edit Configurations -> 添加TomcatServer(Local) -> Server中配置Tomcat路径 -> Deployment中添加Artifact选择java-sec-code:war exploded
```

![tomcat](https://github.com/JoyChou93/java-sec-code/raw/master/idea-tomcat.png)

配置完成后，右上角直接点击run，即可运行。

```
http://localhost:8080/rce/exec?cmd=whoami
```
 
返回

``` 
Viarus
```

## 说明

### 反序列化

利用ysoserial构造POC

``` 
git clone https://github.com/frohoff/ysoserial.git
mvn clean package -DskipTests
java -jar /Users/Viarus/Downloads/ysoserial/target/ysoserial-0.0.6-SNAPSHOT-all.jar CommonsCollections5 'open /Applications/Calculator.app' > /tmp/poc
```

访问`http://localhost:8080/deserialize/test`即可弹窗