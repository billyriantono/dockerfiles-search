FROM ruby:2.5-alpine

# copy patch file
COPY cassandra-web-0.4.0.patch /tmp/cassandra-web-0.4.0.patch

RUN \
    # add runtime dependencies
    apk --no-cache --quiet add libstdc++ && \
    # add build dependencies
    apk --no-cache --quiet --virtual .build-deps add make gcc g++ libc-dev && \
    # install cassandra-web
    gem install cassandra-web  -v 0.4.0 && \
    # apply patch
    patch -p0 < /tmp/cassandra-web-0.4.0.patch && \
    # remove build dependencies
    apk --no-cache --quiet del .build-deps

EXPOSE 3000

ENTRYPOINT ["/usr/local/bundle/bin/cassandra-web"]
