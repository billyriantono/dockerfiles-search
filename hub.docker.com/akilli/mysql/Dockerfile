FROM akilli/base

LABEL maintainer="Ayhan Akilli"

ENV MYPASS=app

# Use mariadb version from V3.10 repository because it does not depend on mariadb-test & co
RUN echo 'http://dl-cdn.alpinelinux.org/alpine/v3.10/main' > /etc/apk/repositories && \
    echo 'http://dl-cdn.alpinelinux.org/alpine/v3.10/community' >> /etc/apk/repositories && \
    apk add --no-cache  \
        mysql \
        mysql-client && \
    rm -rf /var/lib/mysql && \
    mkdir -p \
        /run/mysql \
        /var/log/mysql && \
    chown -R app:app /run/mysql && \
    app-user && \
    app-chown

COPY init/ /init/
COPY s6/ /s6/mysql/
COPY my.cnf /etc/my.cnf
