FROM python:alpine

RUN pip install lizard && \
    apk add --no-cache git openssh-client

WORKDIR /lizard
ENTRYPOINT ["lizard"]
