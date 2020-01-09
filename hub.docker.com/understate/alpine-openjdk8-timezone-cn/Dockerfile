FROM alpine:latest

RUN apk add --update --no-cache openjdk8 && \
    apk add --update --no-cache tzdata && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone && \
    apk del --purge tzdata
    
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
