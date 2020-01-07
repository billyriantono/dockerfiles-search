#
# vizidrix/react-native-android
#
#
# Java 8 JDK / SDK / NDK
#
# React Native
#
#
# VERSION       0.0.2
#

FROM anapsix/alpine-java:jdk
MAINTAINER vizidrix <admin@vizidrix.com>

# Set environment variable to indicate that it is running in CI
ENV CI true

# Install Ant
ENV ANT_VERSION 1.9.7
RUN cd && \
    wget -q http://archive.apache.org/dist/ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz && \
    tar -xzf apache-ant-${ANT_VERSION}-bin.tar.gz && \
    mv apache-ant-${ANT_VERSION} /opt/ant && \
    rm apache-ant-${ANT_VERSION}-bin.tar.gz
ENV ANT_HOME /opt/ant
ENV PATH ${PATH}:/opt/ant/bin

# CMD "sh" "-c" "echo nameserver 8.8.8.8 > /etc/resolv.conf"

# NODE.JS
RUN apk add --update nodejs

RUN npm install -g react-native-cli

CMD [ "react-native", "init", "TestProj" ]
