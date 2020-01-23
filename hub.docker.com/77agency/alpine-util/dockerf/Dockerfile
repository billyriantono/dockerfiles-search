FROM alpine:latest
LABEL Description="Docker image with gosu binary file" Vendor="512k"

ENV GOSU_VERSION="1.11"

RUN set -x \
    && wget -q https://github.com/tianon/gosu/releases/download/${GOSU_VERSION}/gosu-amd64 -O /usr/bin/gosu \
    && chmod +x /usr/bin/gosu \
    && gosu -h

ENTRYPOINT ["/usr/bin/gosu"]
