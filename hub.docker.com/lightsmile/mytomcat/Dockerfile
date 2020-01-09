FROM registry.docker-cn.com/library/tomcat
MAINTAINER lightsmile "bluetears888@126.com"
WORKDIR /usr/local/tomcat_tmp
run wget https://repo1.maven.org/maven2/com/sun/xml/ws/jaxws-ri/2.3.0/jaxws-ri-2.3.0.zip
run unzip jaxws-ri-2.3.0.zip
WORKDIR jaxws-ri
run cp -r ./lib /usr/local/tomcat
WORKDIR /usr/local/tomcat/lib
run rm -r plugins
WORKDIR /usr/local/tomcat
