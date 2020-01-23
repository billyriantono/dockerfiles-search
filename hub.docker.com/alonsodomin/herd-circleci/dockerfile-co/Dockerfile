FROM centos:6.6
MAINTAINER allxone@hotmail.com

# Packages: git
RUN yum -y install wget tar git && yum clean all

# JDK
RUN wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/7u75-b13/jdk-7u75-linux-x64.rpm" && rpm -Uvh jdk-7u75-linux-x64.rpm && rm -f jdk-7u75-linux-x64.rpm && /usr/sbin/alternatives --install "/usr/bin/java" "java" "/usr/java/jdk1.7.0_75/bin/java" 3 && /usr/sbin/alternatives --install "/usr/bin/javac" "javac" "/usr/java/jdk1.7.0_75/bin/javac" 3

# Maven
RUN mkdir -p /usr/local/apache-maven && curl http://mirror.nohup.it/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.tar.gz | tar xz -C /usr/local/apache-maven

# sbt
COPY sbt /root/bin/sbt
RUN chmod u+x ~/bin/sbt && curl -L https://repo.typesafe.com/typesafe/ivy-releases/org.scala-sbt/sbt-launch/0.13.8/sbt-launch.jar?_ga=1.240980167.555107261.1422195821 -o ~/bin/sbt-launch.jar && sh ~/bin/sbt

#ENV
ENV M2_HOME /usr/local/apache-maven/apache-maven-3.3.1
ENV M2 $M2_HOME/bin
ENV PATH $M2:$PATH
ENV JAVA_HOME /usr/java/jdk1.7.0_75
