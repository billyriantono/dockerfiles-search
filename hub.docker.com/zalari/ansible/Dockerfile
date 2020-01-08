FROM alpine:3.8

# install ssh + python
RUN apk --update add openssh && \
    apk --update add python py-pip openssl ca-certificates && \
    apk --update add --virtual build-dependencies \
                python-dev libffi-dev openssl-dev build-base  && \
    pip install --upgrade pip cffi && \
    pip install ansible && \
# remove build-deps after ansible has been installed
    apk del build-dependencies && \
    rm -rf /var/cache/apk/*
