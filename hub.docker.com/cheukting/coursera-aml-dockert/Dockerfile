FROM ubuntu:18.04
  
LABEL maintainer="ChenYu <195936617@qq.com>"

ENV JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"
ENV JRE_HOME=$JAVA_HOME/jre
ENV CLASS_PATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
ENV PATH=${JAVA_HOME}/bin:$PATH

ENV M2_HOME=/root/apache-maven-3.6.1
ENV M2=$M2_HOME/bin
ENV PATH=$M2:$PATH

RUN apt update && \
    apt install git wget openjdk-8-jdk -y && \
    cd /root && \
    git clone https://github.com/wildfirechat/server && \
    wget http://www-eu.apache.org/dist/maven/maven-3/3.6.1/binaries/apache-maven-3.6.1-bin.tar.gz && \
    tar zxvf apache-maven-3.6.1-bin.tar.gz && \
    cd /root/server && \
    mvn clean compile package && \
    mkdir -p /opt/wildfirechat && \
    tar zxvf /root/server/distribution/target/distribution-0.32-bundle-tar.tar.gz -C /opt/wildfirechat && \
    rm -rf /root/*

WORKDIR /opt/wildfirechat

EXPOSE 1883 80 8083 18080

CMD ["sh", "./bin/wildfirechat.sh"]
