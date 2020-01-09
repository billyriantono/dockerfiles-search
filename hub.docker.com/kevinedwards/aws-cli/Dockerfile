FROM alpine:latest

LABEL maintainer="Kevin Edwards <kedwards@kevinedwards.ca>"

ARG AWS_CLI_VERSION=1.16.88

ARG AWS_ACCESS_KEY_ID
ENV AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID

ARG AWS_SECRET_ACCESS_KEY
ENV AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY

ARG AWS_DEFAULT_REGION
ENV AWS_DEFAULT_REGION=$AWS_DEFAULT_REGION

ARG AWS_DEFAULT_OUTPUT
ENV AWS_DEFAULT_OUTPUT=$AWS_DEFAULT_OUTPUT

RUN apk -v --no-cache --update add python py-pip groff less mailcap && \
  pip install --upgrade pip awscli==${AWS_CLI_VERSION} s3cmd python-magic && \
  apk -v --purge del py-pip && \
  rm -rf /var/cache/apk/*

VOLUME /root/.aws \
  /workspace

WORKDIR /workspace

ENTRYPOINT ["aws"]
