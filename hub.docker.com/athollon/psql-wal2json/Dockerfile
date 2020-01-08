FROM postgres:9.6.12-alpine as wal-builder


RUN apk update && apk upgrade && \
    apk add --no-cache git g++ make

RUN git clone https://github.com/eulerto/wal2json -b master --single-branch \
    && cd /wal2json \
    && git checkout 9e962bad61ef2bfa53747470bac4d465e71df880 \
    && make && make install \
    && cd / \
    && rm -rf wal2json

FROM postgres:9.6.12-alpine


COPY --from=wal-builder /usr/local/lib/postgresql /usr/local/lib/postgresql/

# Copy the custom configuration which will be passed down to the server (using a .sample file is the preferred way of doing it by
# the base Docker image)
COPY postgresql.conf.sample /usr/local/share/postgresql/postgresql.conf.sample

# Copy the script which will initialize the replication permissions
COPY ./docker-entrypoint-initdb.d/ /docker-entrypoint-initdb.d
