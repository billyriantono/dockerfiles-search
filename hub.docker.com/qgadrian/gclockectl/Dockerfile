FROM docker:latest

LABEL maintainer=https://github.com/qgadrian

ENV PATH /google-cloud-sdk/bin:$PATH

RUN apk add --update make ca-certificates openssl python gettext \
    && update-ca-certificates \
    && wget https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.tar.gz \
    && tar zxvf google-cloud-sdk.tar.gz \
    && ./google-cloud-sdk/install.sh --usage-reporting=false --path-update=true --additional-components kubectl \
    && rm google-cloud-sdk.tar.gz \
    && gcloud --quiet components update
