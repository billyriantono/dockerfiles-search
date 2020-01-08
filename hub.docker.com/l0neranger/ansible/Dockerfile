FROM python:3.6-alpine

RUN mkdir /etc/ansible/

RUN pip install --upgrade pip \
    && apk add --no-cache \
        bash \
        git \
        sshpass \
        gcc \
        libffi-dev \
        make \
        musl-dev \
        perl \
        postgresql-dev \
    && pip install ansible==2.5.8 \
        boto \
        botocore \
        boto3 \
        psycopg2 \
        awscli

WORKDIR /etc/ansible
