FROM alpine

RUN apk add --no-cache \
    git openssh rsync curl

RUN curl -sSL -o /usr/local/bin/yaml https://github.com/mikefarah/yaml/releases/download/1.13.0/yaml_linux_amd64 \
    && chmod a+x /usr/local/bin/yaml
