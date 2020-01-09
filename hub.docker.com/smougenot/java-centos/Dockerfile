FROM centos:centos7
MAINTAINER sylvain.mougenot@gmail.com

ENV java_url  http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jdk-8u25-linux-x64.rpm

# download and install java
RUN yum install -y wget && \
    wget --no-check-certificate --no-cookies \
      --header "Cookie: oraclelicense=accept-securebackup-cookie" \
      "$java_url" && \
    yum localinstall -y jdk*.rpm && \
    yum clean all && \
	rm -f jdk*.rpm

# alternatives are not in the rpm
RUN alternatives --install /usr/bin/java   java   /usr/java/jdk1.8.0_25/jre/bin/java 1000; \
    alternatives --install /usr/bin/javac  javac  /usr/java/jdk1.8.0_25/jre/bin/javac 1000; \
    alternatives --install /usr/bin/jar    jar    /usr/java/jdk1.8.0_25/jre/bin/jar 1000; \
    alternatives --install /usr/bin/javaws javaws /usr/java/jdk1.8.0_25/jre/bin/jaws 1000
