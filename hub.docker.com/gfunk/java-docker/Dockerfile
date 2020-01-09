FROM gfunk/centos7:latest

# env settings
ENV MAJOR_VERSION 8u144

# Download and install java
RUN yum install -y wget && \
    wget https://mirror.its.sfu.ca/mirror/CentOS-Third-Party/NSG/common/x86_64/jdk-$MAJOR_VERSION-linux-x64.rpm && \
    yum install -y jdk-$MAJOR_VERSION-linux-x64.rpm && \
    rm -f jdk-$MAJOR_VERSION-linux-x64.rpm

# Update alternatives
RUN alternatives --install /usr/bin/java java /usr/java/latest/bin/java 200000 && \
    alternatives --install /usr/bin/javaws javaws /usr/java/latest/bin/javaws 200000 && \
    alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 200000 && \
    alternatives --install /usr/bin/keytool keytool /usr/java/latest/bin/keytool 200000

# Define java_home env
ENV JAVA_HOME /usr/java/latest
