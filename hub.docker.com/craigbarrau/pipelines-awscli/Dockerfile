FROM atlassian/pipelines-awscli

ENV SAM_VERSION=0.15.0

RUN apk --update --no-cache add \
    py-pip \
    gcc \
    musl-dev \
    python-dev  \
    make \
    && pip install --no-cache-dir aws-sam-cli==$SAM_VERSION \
    && apk del py-pip \
    && apk del python-dev \
    && rm -rf /var/cache/apk/* /root/.cache/pip/*
