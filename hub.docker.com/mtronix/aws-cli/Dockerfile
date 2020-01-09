FROM alpine:3.9

WORKDIR /aws

ENV VERSION=1.16.121 \
    AWS_ACCESS_KEY_ID='' \
    AWS_SECRET_ACCESS_KEY='' \
    AWS_SESSION_TOKEN='' \
    AWS_DEFAULT_REGION='' \
    AWS_DEFAULT_OUTPUT='' \
    AWS_DEFAULT_PROFILE='' \
    AWS_CA_BUNDLE='' \
    AWS_SHARED_CREDENTIALS_FILE='' \
    AWS_CONFIG_FILE=''

RUN apk --no-cache --update add bash python3 && \
    pip3 install --upgrade pip && \
    pip3 install --no-cache-dir awscli==${VERSION}

ENTRYPOINT []