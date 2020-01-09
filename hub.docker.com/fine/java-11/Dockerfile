FROM openjdk:11
WORKDIR /usr/src/app
RUN wget http://mirror.bit.edu.cn/apache/maven/maven-3/3.6.1/binaries/apache-maven-3.6.1-bin.zip
RUN unzip apache-maven-3.6.1-bin.zip
RUN mv apache-maven-3.6.1 maven
COPY settings.xml maven/conf
RUN \cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

