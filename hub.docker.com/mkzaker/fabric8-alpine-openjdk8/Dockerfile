FROM fabric8/java-alpine-openjdk8-jdk
MAINTAINER mk.zaker@gmail.com

RUN apk update && apk add tzdata && \
    rm -rf /etc/localtime && \
    cp /usr/share/zoneinfo/Asia/Tehran /etc/localtime && \
    echo "Asia/Tehran" >  /etc/timezone