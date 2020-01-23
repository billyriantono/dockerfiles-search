# 基础镜像
FROM gaoyibing111/baseimage_centosjdk8:3

# 维护者信息
MAINTAINER ybGao <gaoyibing111@126.com>

# springio解释到因为内置到tomcat
VOLUME /tmp

# 将打好的jar 命名为 app.jar 添加到image中
ADD gs-rest-service-0.1.0.jar app.jar

# jdk enviroment
#  如果不添加ENV，下面的 ENTRYPOINT会出现 " exec: \"java\": executable file not found in $PATH " 的错误，且无法启动容器，容器状态为CREATE
ENV JAVA_HOME=/usr/local/jdk/jdk1.8.0_131
ENV PATH=$JAVA_HOME/bin:$PATH

# 每次进入容器后，自动 执行 java  -jar  app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]