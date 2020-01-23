ARG GO_VERSION=1.12.7
FROM golang:$GO_VERSION-alpine AS build

RUN apk add --update bash openssl curl ca-certificates

# Install terraform
ARG TERRAFORM_VERSION=0.12.13
RUN curl -L -sS https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip -o - | unzip -x terraform -d /usr/local/bin/ -

ARG TERRAFORM_PROVIDER_K8S_VERSION=0.1.0
RUN curl -L -sS https://github.com/banzaicloud/terraform-provider-k8s/releases/download/v${TERRAFORM_PROVIDER_K8S_VERSION}/terraform-provider-k8s_${TERRAFORM_PROVIDER_K8S_VERSION}_linux_amd64.tar.gz  -o - | tar -xzvf - -C /usr/local/bin terraform-provider-k8s

# Install kubectl
ARG KUBECTL_VERSION=v1.16.1
RUN curl -L -s https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl

RUN chmod +x /usr/local/bin/*

FROM alpine:3.9

RUN apk add --update bash curl jq

COPY --from=build /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=build /usr/local/bin/terraform* /usr/local/bin/
COPY --from=build /usr/local/bin/kubectl /usr/local/bin/

ADD /terraform/ /terraform

WORKDIR /terraform

RUN terraform init -backend=false

RUN chmod -R ago+rwX /terraform/.terraform