FROM alpine:3.7
MAINTAINER krashekspress
LABEL image=krashekspress/aws-sam

RUN apk --update --no-cache add \
    python \
    py-pip \
    jq \
    bash \
    git \
    groff \
    less \
    mailcap \
    bash \
    gcc \
    python-dev \
    musl-dev \
    && pip install --no-cache-dir awscli==1.16.18 aws-sam-cli==0.16.1 \
    && apk del py-pip \
    && rm -rf /var/cache/apk/* /root/.cache/pip/*

WORKDIR /root
VOLUME /root/.aws

ENTRYPOINT [ "sam" ]
CMD ["--version"]
