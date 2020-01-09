FROM ping2ravi/alpine:latest

RUN apk --no-cache update && \
    apk --no-cache upgrade && \
    apk --no-cache add python py-pip py-setuptools ca-certificates groff less bash && \
    pip --no-cache-dir install awscli --upgrade && \
    rm -rf /var/cache/apk/*

WORKDIR /data

CMD tail -f /dev/null
