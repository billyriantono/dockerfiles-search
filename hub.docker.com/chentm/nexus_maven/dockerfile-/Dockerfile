FROM alpine:3.6
MAINTAINER chengt "1630425@qq.com"

ENV TZ Asia/Shanghai

ENV LANG C.UTF-8

RUN cp /etc/apk/repositories /etc/apk/repositories.bak \
&& echo -e "http://mirrors.aliyun.com/alpine/v3.6/main\nhttp://mirrors.aliyun.com/alpine/v3.6/community" > /etc/apk/repositories \
&& apk update \
&& apk add --no-cache tzdata \
&& ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
&& echo $TZ > /etc/timezone \
&& rm -rf /var/cache/apk/*

CMD ["/bin/ash"]