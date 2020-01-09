FROM alpine:3.8

ENV TERRAFORM_VERSION=0.11.8

# Build-time metadata as defined at http://label-schema.org
ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
ARG REPO_NAME
LABEL org.label-schema.vendor="tmknom" \
      org.label-schema.name=$REPO_NAME \
      org.label-schema.description="Terraform is a tool for building, changing, and combining infrastructure safely and efficiently." \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.version=$VERSION \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/$REPO_NAME" \
      org.label-schema.usage="https://github.com/$REPO_NAME/blob/master/README.md#usage" \
      org.label-schema.docker.cmd="docker run --rm -v \$PWD:/work $REPO_NAME plan" \
      org.label-schema.schema-version="1.0"

WORKDIR /tmp
RUN set -x && \
    apk add --no-cache git=2.18.0-r0 unzip=6.0-r4 wget=1.19.5-r0 && \
    wget https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
    unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip -d / && \
    apk del --purge unzip wget && \
    rm -rf /tmp/*

WORKDIR /work
ENTRYPOINT ["/terraform"]
CMD ["--help"]
