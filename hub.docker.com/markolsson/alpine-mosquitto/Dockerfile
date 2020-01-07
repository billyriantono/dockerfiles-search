FROM alpine:3.4
MAINTAINER Mark Olsson <post@markolsson.se>

RUN apk --update add mosquitto && \
	rm /var/cache/apk/*

EXPOSE 1883

CMD ["/usr/sbin/mosquitto"]
