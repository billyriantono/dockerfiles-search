FROM alpine:latest
MAINTAINER ksh2ksk4 <ksh2ksk4+docker.com@gmail.com>

ENV TIMEZONE='Asia/Tokyo' \
    DISTRIBUTIONS="./distributions"

WORKDIR /root

RUN apk update && \
    apk upgrade && \
    # Change the timezone
    apk add tzdata && \
    cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
    echo "${TIMEZONE}" >/etc/timezone && \
    # Install some packages
    apk add --virtual _mariadb-packages_ \
        mariadb \
        mariadb-client && \
    apk add --virtual _base-packages_ \
        bash \
        file \
        findutils \
        less

COPY ${DISTRIBUTIONS}/root/* /root/
COPY ${DISTRIBUTIONS}/mariadb/my.cnf /etc/mysql/

RUN mysql_install_db --user=mysql

VOLUME /var/lib/mysql

EXPOSE 3306

ENTRYPOINT ["./entrypoint.sh"]
