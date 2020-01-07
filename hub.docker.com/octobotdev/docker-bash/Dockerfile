FROM docker:stable

RUN apk add --no-cache bash py3-pip python3-dev libffi-dev openssl-dev gcc libc-dev make git && \
    pip3 install docker-compose && \
    apk del python3-dev libffi-dev openssl-dev gcc libc-dev make