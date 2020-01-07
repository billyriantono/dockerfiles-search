FROM php:5.6-alpine3.8
MAINTAINER mlch911 <mlch911@mluoc.tech>

RUN apk add git tzdata && \
	git clone https://github.com/mlch911/freenom.git && \
	cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
	apk del tzdata git && \
	mkdir -p mlch911 && \
	cp /freenom/config.php /mlch911/ && \
	rm -rf /freenom/config.php && \
	echo '00 08 * * * cd /freenom/; php index.php >/dev/null 2>&1'>>/var/spool/cron/crontabs/root

VOLUME ["/conf"]
RUN cp -u /mlch911/config.php /conf && \
	cp /conf/config.php /freenom && \
	crond
