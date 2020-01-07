FROM docker:stable

RUN apk update
RUN apk upgrade
RUN apk add python3 python3-dev build-base libffi-dev openssl-dev bash haproxy curl jq
RUN pip3 install docker-compose
