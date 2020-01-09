FROM alpine:3.4
MAINTAINER r.schouw@portbase.com

RUN apk add --no-cache --update bash curl tzdata && \
    cp /usr/share/zoneinfo/Europe/Amsterdam /etc/localtime && \
    curl -S -o /ecs-cli https://s3.amazonaws.com/amazon-ecs-cli/ecs-cli-linux-amd64-latest && \
    chmod 755 /ecs-cli


ENTRYPOINT ["/ecs-cli"]
