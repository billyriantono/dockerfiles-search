FROM python:alpine3.6

RUN apk -U add ca-certificates build-base git openssh && \
    pip install pipenv && \
    rm -r /var/cache/apk/* && \
    mkdir /app

WORKDIR /app

ADD docker-entrypoint.sh /docker-entrypoint.sh

ENTRYPOINT [ "/docker-entrypoint.sh" ]
