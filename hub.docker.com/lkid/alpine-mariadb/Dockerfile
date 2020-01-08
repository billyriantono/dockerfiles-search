FROM lkid/alpine-base:latest
MAINTAINER LKiD


RUN apk add --update mariadb mariadb-client bash && \
    rm -rf /var/cache/apk/* && \
    mkdir -p /var/run/mysqld/ && \
    chown mysql:mysql /var/lib/mysql


# Add the files
ADD root /

VOLUME ["/var/lib/mysql", "/var/lib/backup"]

# Expose the ports for mysql
EXPOSE 3306
