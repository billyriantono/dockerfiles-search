FROM alpine:3.4
MAINTAINER Linus Gubenis

RUN apk add --no-cache \
  bash \
  curl \
  git \
  python \
  nodejs \
  openssh-client \
  py-pip && \
  pip install --upgrade awscli && \
  npm install -g serverless@0.5

ENTRYPOINT ["bash"]
