FROM alpine:3.5

RUN apk update && \
    apk upgrade && \
    addgroup -S mysql && \
    adduser -S mysql -G mysql && \
    apk add --no-cache \
        mysql \
        mysql-client \
        && \
    /usr/bin/mysql_install_db --user=mysql && \
    rm -frv /var/cache/apk/*

EXPOSE 3306
ENTRYPOINT ["mysqld "]
CMD ["--user=mysql", "--console"]
