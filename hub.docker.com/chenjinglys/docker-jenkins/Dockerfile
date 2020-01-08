FROM jenkins/jenkins:2.164.1

MAINTAINER by chenjing (chenjinglys@163.com)
ENV TZ Asia/Shanghai

USER root
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

#清除了基础镜像设置的源，切换成阿里云的jessie源
RUN echo '' > /etc/apt/sources.list.d/jessie-backports.list \
  && echo "deb http://mirrors.aliyun.com/debian jessie main contrib non-free" > /etc/apt/sources.list \
  && echo "deb http://mirrors.aliyun.com/debian jessie-updates main contrib non-free" >> /etc/apt/sources.list \
  && echo "deb http://mirrors.aliyun.com/debian-security jessie/updates main contrib non-free" >> /etc/apt/sources.list
#更新源并安装缺少的包
RUN apt-get update && apt-get install -y libltdl7 && apt-get update

ARG dockerGid=999

RUN echo "docker:x:${dockerGid}:jenkins" >> /etc/group \

# install wget
RUN apt-get install -y wget
#RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
## ---------------------------------------------------------------------
# get maven 3.5.4
RUN wget --no-verbose -O /tmp/apache-maven-3.5.4-bin.tar.gz http://apache.cs.utah.edu/maven/maven-3/3.5.4/binaries/apache-maven-3.5.4-bin.tar.gz
# install maven
RUN tar xzf /tmp/apache-maven-3.5.4-bin.tar.gz -C /opt/
RUN ln -s /opt/apache-maven-3.5.4 /opt/maven
RUN ln -s /opt/maven/bin/mvn /usr/local/bin
RUN rm -f /tmp/apache-maven-3.5.4-bin.tar.gz
ENV MAVEN_HOME /opt/maven

RUN chown -R jenkins:jenkins /opt/maven
## ---------------------------------------------------------------------

## ---------------------------------------------------------------------
RUN wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jdk-8u201-linux-x64.tar.gz
# install jdk
RUN tar -zxvf jdk-8u201-linux-x64.tar.gz -C /opt/
RUN ln -s /opt/jdk1.8.0_201 /opt/jdk8
RUN rm -f /tmp/jdk-8u201-linux-x64.tar.gz

ENV  JAVA_HOME=/opt/jdk8
ENV  JRE_HOME=$JAVA_HOME/jre \
     PATH=$JAVA_HOME/bin:$PATH \
     CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOEM/lib/tools.jar

RUN chown -R jenkins:jenkins /opt/jdk8
## ---------------------------------------------------------------------

# remove download archive files
RUN apt-get clean

RUN usermod -aG docker jenkins
USER jenkins


#https://github.com/mkheck/jenkins/blob/master/Dockerfile
