FROM golang:1.10-alpine3.8 as build

ENV APP_ROOT /go/src/github.com/Growth-Hack-Studio/ascii-club-free-api-server
WORKDIR $APP_ROOT

COPY . $APP_ROOT

RUN apk update && \
    apk add --no-cache git && \
    go get -u github.com/golang/dep/... && \
    rm -rf /var/cache/apk/* && \
    dep ensure && \
    go build -o ${APP_ROOT}/api .

FROM openjdk:8-jdk-alpine3.8

ENV DIGDAG_VERSION=0.9.31

RUN apk add --no-cache curl && \
    curl -o /usr/bin/digdag --create-dirs -L "https://dl.digdag.io/digdag-$DIGDAG_VERSION" && \
    chmod +x /usr/bin/digdag && \
    apk del curl && \
    adduser -h /var/lib/digdag -g 'digdag user' -s /sbin/nologin -D digdag && \
    mkdir -p /var/lib/digdag/logs/tasks /var/lib/digdag/logs/server && \
    chown -R digdag.digdag /var/lib/digdag && \
    \
    apk --no-cache update && \
    apk --no-cache add python py-pip py-setuptools ca-certificates curl groff less && \
    apk --no-cache add bash jq && \
    apk --no-cache add openrc && \
    pip --no-cache-dir install awscli && \
    pip install awscli && \
    rm -rf /var/cache/apk/*

COPY --from=build /go/src/github.com/Growth-Hack-Studio/ascii-club-free-api-server/api /usr/local/bin/api

CMD ["/usr/local/bin/api"]