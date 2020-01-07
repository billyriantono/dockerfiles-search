FROM jasonzou/alpine-base:latest
MAINTAINER Jason Zou <jason.zou@gmail.com>

RUN apk add --update mariadb mariadb-common mariadb-client && \
    rm -rf /var/cache/apk/*

# copy configuration files
COPY root /

# EntryPoint
ENTRYPOINT ["/init"]

CMD []

# Expose port
EXPOSE 3306

# Volume
VOLUME ["/var/lib/mysql"]
