FROM alpine:3.8

LABEL maintainer="Ben Roberts <ben@headsnet.com>"

WORKDIR /app
VOLUME /app
COPY scripts/startup.sh /startup.sh

RUN apk --no-cache add \
	  mysql \
	  mysql-client

COPY my.cnf /etc/mysql/my.cnf

RUN addgroup -g 1000 -S app && \
    adduser -u 1000 -S app -G app

EXPOSE 3306

USER app

CMD ["/startup.sh"]
