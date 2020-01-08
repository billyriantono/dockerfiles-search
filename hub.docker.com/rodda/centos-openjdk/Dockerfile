FROM centos:7

MAINTAINER Gayan Rodrigo madushan.gayan@gmail.com

ENV JAVA_VER=11.0.1

#Install Packages
RUN yum update -y
RUN yum install -y wget
RUN wget https://download.java.net/java/GA/jdk11/13/GPL/openjdk-${JAVA_VER}_linux-x64_bin.tar.gz -O /opt/jdk${JAVA_VER}.tar.gz

RUN cd /opt; \
tar -xzvf jdk${JAVA_VER}.tar.gz; \
rm jdk${JAVA_VER}.tar.gz

RUN cd /opt/jdk-${JAVA_VER}; \
alternatives --install /usr/bin/java java /opt/jdk-${JAVA_VER}/bin/java 2
RUN yum clean all

ENV JAVA_HOME=/opt/jdk-${JAVA_VER}
ENV JRE_HOME $JAVA_HOME/jre
ENV PATH $JAVA_HOME/bin:$PATH
RUN export PATH

CMD ["/bin/bash"]