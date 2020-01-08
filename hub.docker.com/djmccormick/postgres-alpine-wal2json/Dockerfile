FROM postgres:11-alpine

ENV WAL2JSON_COMMIT_ID=72e3a2e952c438f24b63cb53cb328f33ec396f4f

RUN apk update
RUN apk add --no-cache --virtual .build-deps gcc git make musl-dev pkgconf \
    && git clone https://github.com/eulerto/wal2json -b master --single-branch \
    && (cd /wal2json && git checkout $WAL2JSON_COMMIT_ID && USE_PGXS=1 make && USE_PGXS=1 make install) \
    && rm -rf wal2json \
    && apk del .build-deps

COPY /docker-entrypoint-initdb.d /docker-entrypoint-initdb.d
