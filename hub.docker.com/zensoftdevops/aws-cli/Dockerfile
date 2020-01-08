FROM alpine:3.7

ENV PAGER="more"

RUN apk --no-cache add \
      bash \
      curl \
      jq \
      groff \
      py-pip \
      python &&\
    pip install --upgrade \
      pip \
      awscli &&\
    mkdir ~/.aws

# Expose volume for adding credentials
VOLUME ["~/.aws"]
