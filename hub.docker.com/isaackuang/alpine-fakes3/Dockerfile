FROM isaackuang/alpine-base:3.8.0

RUN apk --no-cache --progress add \
    ca-certificates ruby ruby-io-console ruby-webrick ruby-etc && \
    gem install --no-rdoc --no-ri fakes3 && \
    mkdir -p /fakes3/data

ADD config /
