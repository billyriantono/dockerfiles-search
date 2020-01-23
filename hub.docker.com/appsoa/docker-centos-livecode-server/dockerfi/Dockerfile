FROM python:2-alpine

RUN apk add --no-cache \
    ca-certificates wget curl git openssh jq npm nodejs docker \
    && update-ca-certificates \
    && pip install flake8 awscli docker-compose
