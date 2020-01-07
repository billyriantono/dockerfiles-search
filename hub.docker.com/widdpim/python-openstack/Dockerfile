FROM jfloff/alpine-python:latest

RUN apk add --update libffi-dev openssl-dev && \
    pip install python-openstackclient && \
    rm -rf /var/cache/apk/*

ENTRYPOINT ["openstack"]
