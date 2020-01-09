FROM alpine:latest
MAINTAINER Tiga love_internet@foxmail.com

ENV  TIME_ZONE Asia/Shanghai

RUN apk update \
&& apk add openntpd \
&& apk add tzdata \ 
&& echo "${TIME_ZONE}" > /etc/timezone \
&& ln -fs /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime 
ADD ntpd.conf /etc/


EXPOSE 123/udp

ENTRYPOINT ["/usr/sbin/ntpd"]
CMD ["-d"]
