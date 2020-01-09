FROM	alpine:3.6
MAINTAINER Mikolaj Rydzewski <mikolaj.rydzewski@gmail.com>
RUN	apk update && \
	apk add squid && \
	rm -rf /var/cache/apk
CMD	["/usr/sbin/squid", "-N"]
EXPOSE	3128
COPY	squid.conf /etc/squid/
