FROM alpine

ENV TZ "Asia/Shanghai"
ENV PS1 "\[\033[0;32m\]\A \[\033[0;31m\]\u\[\033[0;34m\]@\[\033[0;35m\]\h\[\033[0;34m\]:\[\033[00;36m\]\w\[\033[0;33m\] -> \$ \[\033[0m\] "

RUN apk add --update \
    bash \
    openjdk8-jre-base \
    && rm -rf /var/cache/apk/*

ENV JAVA_HOME /usr/lib/jvm/default-jvm
ENV PATH ${PATH}:${JAVA_HOME}/bin

CMD "/bin/bash"