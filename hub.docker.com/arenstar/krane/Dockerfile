FROM alpine:3.8 as builder
ARG K8S_VERSION=v1.16.3
RUN set -x                  && \
    apk --update upgrade    && \
    apk add ca-certificates && \
    rm -rf /var/cache/apk/* && \
    wget -O /kubectl https://storage.googleapis.com/kubernetes-release/release/$K8S_VERSION/bin/linux/amd64/kubectl && \
    chmod +x /kubectl

FROM google/cloud-sdk:alpine

COPY --from=builder /kubectl /kubectl

RUN apk add --update \
  bash \
  build-base \
  ca-certificates \
  gcc \
  ruby \
  ruby-bundler \
  ruby-dev \
  && rm -rf /var/cache/apk/* \
  && gem install krane --no-document

CMD bash