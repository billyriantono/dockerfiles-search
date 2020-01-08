FROM frolvlad/alpine-oraclejre8
MAINTAINER wangshun <wangshun@wangshun.org>

ENV JAVA_OPTS="$JAVA_OPTS -Dsun.jnu.encoding=UTF-8 -Dfile.encoding=UTF-8 -Djava.security.egd=file:/dev/./urandom " \
    JAVA_HOME=$JAVA_HOME/jre
RUN echo "http://mirrors.aliyun.com/alpine/v3.8/main" > /etc/apk/repositories \
    && echo "http://mirrors.aliyun.com/alpine/v3.8/community" >> /etc/apk/repositories \
    && apk update upgrade \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone