FROM kong:0.14.1-centos

LABEL maintainer "Zhaoweidong <zhaoweidong@gouuse.cn>"

ENV TIMEZONE Asia/Shanghai

RUN set -ex \
##### Modify timezone.
    && ln -snf /usr/share/zoneinfo/$TIMEZONE /etc/localtime \
    && echo $TIMEZONE >/etc/timezone \
##### Add script.
    && mkdir /apps \
    && curl -o /apps/run.sh https://raw.githubusercontent.com/1993Plus/docker-kong/master/run.sh \
    && chmod +x /apps/run.sh
