FROM alpine:3.7
MAINTAINER djmattyg007

ENV VERSION=2018.01.22-1

RUN apk --update add graphviz ttf-dejavu && \
    rm -rf /var/cache/apk/*

COPY graphviz-server /usr/local/bin/graphviz-server

EXPOSE 8000
ENTRYPOINT ["/usr/local/bin/graphviz-server"]
