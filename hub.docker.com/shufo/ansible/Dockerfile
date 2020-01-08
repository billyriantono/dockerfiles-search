FROM alpine:3.3

MAINTAINER shufo

ENV ANSIBLE_VERSION 2.0.2.0

RUN apk add --update --no-cache python-dev py-pip gcc musl-dev openssl-dev libffi-dev && \
    pip install ansible==$ANSIBLE_VERSION

ENTRYPOINT ["ansible"]
CMD ["--help"]
