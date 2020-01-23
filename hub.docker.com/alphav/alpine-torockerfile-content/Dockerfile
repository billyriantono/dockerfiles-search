FROM alpine:3.8

RUN apk update && \
    apk add bash curl && \
    curl -o /usr/local/bin/ecs-cli https://amazon-ecs-cli.s3.amazonaws.com/ecs-cli-linux-amd64-latest && \
    chmod +x /usr/local/bin/ecs-cli

COPY pipe.sh /

ENTRYPOINT ["/pipe.sh"]