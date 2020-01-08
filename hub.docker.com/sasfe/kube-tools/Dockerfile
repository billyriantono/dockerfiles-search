FROM google/cloud-sdk:alpine
LABEL maintainer="zhao.lang@sas.com"

RUN apk update \
    && apk add curl jq \
    && rm -rf /var/cache/apk/*

RUN gcloud components install gsutil kubectl

CMD ["/bin/sh"]