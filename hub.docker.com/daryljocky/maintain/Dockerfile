FROM python:3.5-alpine3.9

RUN apk add --no-cache mysql-client mariadb-backup bash && \
    apk add --virtual BUILD curl && \
    curl -fSL "https://github.com/Flowman/pxc-alpine/releases/download/5.7.16-27.19/percona-xtrabackup-2.4.6-r0.apk" -o "percona-xtrabackup-2.4.6-r0.apk" && \
    apk add --allow-untrusted percona-xtrabackup-2.4.6-r0.apk && \
    apk del BUILD

RUN pip install --no-cache-dir docker colorama  

ADD qpress /usr/bin/qpress
