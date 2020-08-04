# 源码构建

下载地址：https://tomcat.apache.org/download-80.cgi

# 配置

1.解压源码 apache-tomcat-8.5.57-src

2.apache-tomcat-8.5.57-src目录下添加pom文件

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>
    <groupId>org.apache.tomcat</groupId>
    <artifactId>Tomcat8.0</artifactId>
    <name>Tomcat8.0</name>
    <version>8.0</version>

    <build>
        <finalName>Tomcat8.0</finalName>
        <sourceDirectory>java</sourceDirectory>
        <testSourceDirectory>test</testSourceDirectory>
        <resources>
            <resource>
                <directory>java</directory>
            </resource>
        </resources>
        <testResources>
            <testResource>
                <directory>test</directory>
            </testResource>
        </testResources>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <encoding>UTF-8</encoding>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.easymock</groupId>
            <artifactId>easymock</artifactId>
            <version>3.4</version>
        </dependency>
        <dependency>
            <groupId>ant</groupId>
            <artifactId>ant</artifactId>
            <version>1.7.0</version>
        </dependency>
        <dependency>
            <groupId>wsdl4j</groupId>
            <artifactId>wsdl4j</artifactId>
            <version>1.6.2</version>
        </dependency>
        <dependency>
            <groupId>javax.xml</groupId>
            <artifactId>jaxrpc</artifactId>
            <version>1.1</version>
        </dependency>
        <dependency>
            <groupId>org.eclipse.jdt.core.compiler</groupId>
            <artifactId>ecj</artifactId>
            <version>4.5.1</version>
        </dependency>

    </dependencies>
</project>
```

3.在apache-tomcat-8.5.57-src 同级目录新建 catalina-home并保证目录下面文件



**注意：** 上面文件夹apache-tomcat-8.5.57-src里面有的，就剪切过来，没有的就新建一个， bin conf webapps 应该是从apache-tomcat-8.5.57-src剪切过来的

4.idea引入项目

File->Open 选择解压的C:\Users\wukong\Downloads\apache-tomcat-8.5.57-src\apache-tomcat-8.5.57-src



# **配置启动**

1. MainClass: org.apache.catalina.startup.Bootstrap
2. VmOptions: -Dcatalina.home=C:\Users\wukong\Downloads\apache-tomcat-8.5.57-src\apache-tomcat-8.5.57-src\catalina-home

# **启动报错**

TestCookieFilter 报错找不到这个类CookieFilter

解决方法：

1. 删除：TestCookieFilter



启动后，访问localhost:8080 报错 org.apache.jasper.JasperException: java.lang.NullPointerException

解决方案：

org.apache.catalina.startup.Bootstrap 添加代码块

```
{
        JasperInitializer initializer =new JasperInitializer();
  }
```


