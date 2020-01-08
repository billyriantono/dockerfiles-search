FROM node:10-alpine
LABEL maintainer="SungKwang Song<tech@sungkwang.me>"

RUN apk --no-cache --update add build-base libffi-dev git py-pip openssh-keygen openssh-client
RUN pip install --upgrade pip
RUN pip install awscli
RUN pip install awsebcli
RUN mkdir -p /var/app/current
WORKDIR /var/app/current


