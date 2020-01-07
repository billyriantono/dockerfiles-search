FROM golang:1.12.7-alpine3.10

ENV TZ=Asia/Shanghai

RUN set -e \
&& apk add --no-cache tzdata \
&& ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
&& echo $TZ > /etc/timezone
