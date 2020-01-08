FROM maven:3.6.1-jdk-8-alpine

ENV TZ="Asia/Shanghai"

RUN set -e \
&& apk add --no-cache tzdata \
&& ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
&& echo $TZ > /etc/timezone
