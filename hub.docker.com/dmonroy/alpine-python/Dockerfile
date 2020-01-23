FROM alpine:latest


RUN apk add --update \
    python \
    python-dev \
    py-pip \
    && pip install --upgrade pip \
    && rm /var/cache/apk/*

CMD python