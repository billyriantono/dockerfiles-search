# vim: set ts=4 sw=4 tw=0 et

FROM alpine:3.8
MAINTAINER Grzegorz Adamowicz

ARG VERSION=0.11.8
ARG RELEASES_URL=https://releases.hashicorp.com
ARG TERRAFORM_FILENAME=terraform_${VERSION}_linux_amd64.zip
ENV TERRAFORM_VERSION $VERSION

LABEL Description="Terraform"

RUN apk update && apk upgrade && \
    apk add bash ca-certificates && \
    cd /tmp && \
    wget --quiet ${RELEASES_URL}/terraform/${TERRAFORM_VERSION}/${TERRAFORM_FILENAME} && \
    unzip ${TERRAFORM_FILENAME} && \
    mv /tmp/terraform /usr/local/bin/ && \
    rm -f /tmp/terraform*zip && \
    rm -rf /var/cache/apk/*

ENTRYPOINT ["/usr/local/bin/terraform"]
CMD ["version"]
