FROM alpine:3.4
LABEL maintainer="Denis Arosquipa <darosquipa@dtransforma.com>"

RUN apk update && \
	apk add mysql mysql-client && \
	addgroup mysql mysql && \
	mkdir /scripts && \
	rm -rf /var/cache/apk/*

VOLUME ["/var/lib/mysql"]

ADD my.cnf /etc/mysql/my.cnf

ADD startup.sh /scripts/startup.sh

RUN chmod +x /scripts/startup.sh

EXPOSE 3306

ENTRYPOINT ["/scripts/startup.sh"]
