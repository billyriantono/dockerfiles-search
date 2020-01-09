FROM openjdk:8-jdk-alpine
VOLUME /tmp

RUN apk --no-cache add tzdata ttf-dejavu && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone
    
