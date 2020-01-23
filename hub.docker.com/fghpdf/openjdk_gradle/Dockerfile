FROM openjdk:8
MAINTAINER fghpdf <quxiangxuanqxx@gmail.com>

RUN \
    cd /usr/local && \
    curl -L https://services.gradle.org/distributions/gradle-3.5-bin.zip -o gradle-3.5-bin.zip && \
    unzip gradle-3.5-bin.zip && \
    rm gradle-3.5-bin.zip
    
ENV GRADLE_HOME=/usr/local/gradle-3.5
ENV PATH=$PATH:$GRADLE_HOME/bin JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64

