FROM rabbitmq:3.7.15-management-alpine

ENV TZ="Asia/Shanghai"

RUN set -e \
&& apk add --no-cache tzdata \
&& ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
&& echo $TZ > /etc/timezone
