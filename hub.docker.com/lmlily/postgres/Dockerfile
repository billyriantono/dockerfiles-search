FROM postgres:11.3-alpine

ENV TZ="Asia/Shanghai"

RUN set -e \
&& apk add --no-cache tzdata \
&& ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
&& echo $TZ > /etc/timezone
