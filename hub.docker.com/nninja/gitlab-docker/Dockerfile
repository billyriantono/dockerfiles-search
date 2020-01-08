FROM docker:stable

RUN apk add --update make curl ncurses git

RUN apk add --update py-pip python-dev libffi-dev openssl-dev gcc libc-dev make \
    && pip install docker-compose

ENV PATH="/usr/local/bin:${PATH}"
