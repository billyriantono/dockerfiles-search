FROM centos:7

ENV JAVA_VERSION 8u162
ENV BUILD_VERSION b12
ENV HASH_CODE 0da788060d494f5095bf8624735fa2f1

#RUN wget --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" \
#        "http://download.oracle.com/otn-pub/java/jdk/$JAVA_VERSION-$BUILD_VERSION/$HASH_CODE/jdk-$JAVA_VERSION-linux-x64.rpm" \
#        -O /tmp/jdk-8-linux-x64.rpm \
#    && yum -y install /tmp/jdk-linux-x64.rpm \
#    && rm -rf /tmp/jdk-linux-x64.rpm \
#    && yum clean all \
#    && rm -rf /var/cache/yum

RUN curl -v -j -k -L -H "Cookie: oraclelicense=accept-securebackup-cookie" \
        "http://download.oracle.com/otn-pub/java/jdk/$JAVA_VERSION-$BUILD_VERSION/$HASH_CODE/jdk-$JAVA_VERSION-linux-x64.rpm" \
      -o /tmp/jdk-linux-x64.rpm \
    && yum -y install /tmp/jdk-linux-x64.rpm \
    && rm -rf /tmp/jdk-linux-x64.rpm \
    && yum clean all \
    && rm -rf /var/cache/yum

# RUN curl -v -j -k -L -H  "Cookie: oraclelicense=accept-securebackup-cookie" \
#        http://download.oracle.com/otn-pub/java/jdk/9.0.4+11/c2514751926b4512b076cc82f959763f/jdk-9.0.4_linux-x64_bin.rpm \
#        -o /tmp/jdk-linux-x64.rpm
#    && yum -y install /tmp/jdk-linux-x64.rpm \
#    && rm -rf /tmp/jdk-linux-x64.rpm \
#    && yum clean all \
#    && rm -rf /var/cache/yum


RUN alternatives --install /usr/bin/java java /usr/java/latest/bin/java 200000 \
    && alternatives --install /usr/bin/javaws javaws /usr/java/latest/bin/javaws 200000 \
    && alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 200000 \
    && alternatives --install /usr/bin/keytool keytool /usr/java/latest/bin/keytool 200000

ENV JAVA_HOME /usr/java/latest
