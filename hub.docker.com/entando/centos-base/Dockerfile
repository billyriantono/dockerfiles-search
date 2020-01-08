FROM centos:7
LABEL MAINTAINER="Pietrangelo Masala <p.masala@entando.com>"
USER root
ENV LC_ALL en_US.UTF-8
ENV MAVEN_VERSION 3.3.9
ENV JAVA_HOME /usr/lib/jvm/java
ENV JRE_HOME /usr/lib/jvm/jre
ENV MAVEN_HOME /usr/share/maven

RUN yum install -y curl git ImageMagick java-1.8.0-openjdk-devel \
&& adduser entando \
&& cd /tmp \
&& mkdir -p /usr/share/maven \
&& curl -fsSL http://apache.osuosl.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
| tar -xzC /usr/share/maven --strip-components=1 \
&& ln -s /usr/share/maven/bin/mvn /usr/bin/mvn \
&& yum clean all