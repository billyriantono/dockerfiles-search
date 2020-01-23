FROM alpine as base
FROM base as builder

MAINTAINER Fisher Pri Catz "fisher.wei@wqfw.de"

RUN apk update && apk upgrade && \
    apk add --no-cache mysql-client

WORKDIR /mysqldump

ENTRYPOINT ["sh", "-c", "mysqldump -u$DB_USER -p$DB_PASS --host=$DB_HOST --databases $DB_DB --hex-blob 2>/mysqldump/$(date +'%Y%m%d_%H%M%S')_err.log | gzip > /mysqldump/$(date +'%Y%m%d_%H%M%S').sql.gz "]


