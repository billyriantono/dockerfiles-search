FROM alpine:latest

RUN apk --no-cache update && \
    apk --no-cache add python py-pip py-setuptools parallel ca-certificates zip curl groff less jq git openssh && \
    pip --no-cache-dir install awscli && \
    rm -rf /var/cache/apk/* && \
    apk -v --purge del py-pip