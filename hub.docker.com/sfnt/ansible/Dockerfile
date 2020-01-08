FROM alpine:3.9
ENV ANSIBLE_VERSION=2.7.7
ENV PY_WINRM_VERSION=0.3.0
RUN set -xe && \
    apk add --no-cache --progress python py-pip openssl ca-certificates git openssh sshpass && \
    apk --update add --virtual build-dependencies python-dev libffi-dev openssl-dev build-base && \
    pip install --upgrade pip && \
    pip install ansible==${ANSIBLE_VERSION} && \
    pip install pywinrm>=${PY_WINRM_VERSION} && \
    apk del build-dependencies && \
    rm -rf /var/cache/apk/*
