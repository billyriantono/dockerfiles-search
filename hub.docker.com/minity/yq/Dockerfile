FROM alpine
LABEL maintainer="anton@tyutin.ru"

RUN apk add --no-cache py2-pip jq && pip install -q yq

ENTRYPOINT ["/usr/bin/yq"]
