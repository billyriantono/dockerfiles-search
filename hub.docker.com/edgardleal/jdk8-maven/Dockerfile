
# Eclipse-Che ide server
# 17/04/2016

FROM edgardleal/jdk8
MAINTAINER Edgard Leal <edgardleal@gmail.com>

RUN yum -y update && yum -y install git-core && yum clean all

ENV JAVA_HOME /usr/java/jdk1.8.0_40/
RUN useradd java

USER java
WORKDIR "/home/java"

RUN ["/usr/bin/wget", "http://mirror.nbtelecom.com.br/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.zip"]
RUN ["unzip", "apache-maven-3.3.9-bin.zip", "-d", ".apps"]
RUN ["rm", "-f", "apache-maven-3.3.9-bin.zip"]
ENV PATH "${PATH}:/home/java/.apps/apache-maven-3.3.9/bin/"

RUN ["echo", "****************************************"]
RUN ["mvn", "-v"]
RUN ["echo", "****************************************"]


RUN ["java","-version"]
CMD "mvn -v"
