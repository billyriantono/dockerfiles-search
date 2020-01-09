FROM python:3.6.8-alpine3.10

LABEL Author "fortejas@amazon.com"

ARG VERSION=0.0.2

RUN python -m pip install \
        awscli==1.16.286 \
        kubediag==${VERSION} \
        pip==19.3.1

ENTRYPOINT ["/usr/local/bin/kubediag"]