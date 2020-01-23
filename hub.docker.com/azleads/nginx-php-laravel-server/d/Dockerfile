FROM alpine:3.9.2
MAINTAINER ayunyan <ayunyan@gmail.com>

ENV KUBERNETES_VERSION=v1.13.4

RUN apk add --no-cache ca-certificates && update-ca-certificates && \
    wget https://storage.googleapis.com/kubernetes-release/release/${KUBERNETES_VERSION}/bin/linux/amd64/kubectl && \
    chmod 755 kubectl && \
    mv kubectl /bin/kubectl

