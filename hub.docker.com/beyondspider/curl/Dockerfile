FROM alpine:latest
MAINTAINER from www.beyondspider.com by admin (admin@beyondspider.com)

ENV TIME_ZONE Asia/Shanghai
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories && \
	apk add --update curl && rm -rf /var/cache/apk/* && \
	ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime

COPY entrypoint.sh /
RUN chmod 777 /*.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD ["curl"]
