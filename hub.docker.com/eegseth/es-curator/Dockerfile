FROM alpine
MAINTAINER EE
RUN apk --update add python py-setuptools py-pip && \
    pip install elasticsearch-curator==5.2.0 && \
    pip install requests-aws4auth && \
    apk del py-pip && \
    rm -rf /var/cache/apk/*
USER nobody:nobody
ENTRYPOINT ["/bin/sh"]
