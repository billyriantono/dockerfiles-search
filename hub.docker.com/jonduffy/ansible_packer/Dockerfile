FROM golang:alpine

env USER root

ENV PACKER_VERSION=1.4.0
ENV PACKER_SHA256SUM=73074f4fa07fe15b5d65a694ee7afae2d1a64f0287e6b40897adee77a7afc552

RUN apk --update upgrade

RUN apk add --update git bash wget openssl

ADD https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip ./
ADD https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_SHA256SUMS ./

RUN sed -i '/.*linux_amd64.zip/!d' packer_${PACKER_VERSION}_SHA256SUMS
RUN sha256sum -cs packer_${PACKER_VERSION}_SHA256SUMS
RUN unzip packer_${PACKER_VERSION}_linux_amd64.zip -d /bin
RUN rm -f packer_${PACKER_VERSION}_linux_amd64.zip

RUN apk update
RUN apk add python3 py-pip jq gcc python3-dev musl-dev libffi-dev build-base make openssl-dev
RUN pip3 install --upgrade awscli
RUN pip3 install --upgrade pip
RUN pip3 install --upgrade ansible
RUN pip3 install cryptography==2.6.1

RUN apk --no-cache add ca-certificates && update-ca-certificates && ls -al /etc/ssl/

RUN apk add openssh
RUN echo "Host *" >> /etc/ssh/ssh_config
RUN echo "    SendEnv LANG LC_*" >> /etc/ssh/ssh_config

RUN addgroup -S alpine && adduser -S alpine -G alpine

RUN chown alpine:alpine /etc/ssl/certs/

USER alpine
WORKDIR /home/alpine