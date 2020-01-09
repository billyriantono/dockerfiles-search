FROM golang:latest
LABEL maintainer="Terraformation Team <terraformation.docker@outlook.com>"

ENV TERRAFORM_VERSION=0.12.13
ENV TERRAFORM_SHA256SUM=b337c885526a8a653075551ac5363a09925ce9cf141f4e9a0d9f497842c85ad5
RUN apt-get update && apt-get install git bash wget curl zip -y
RUN wget https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip
RUN wget https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_SHA256SUMS
RUN sed -i "/terraform_${TERRAFORM_VERSION}_linux_amd64.zip/!d" terraform_${TERRAFORM_VERSION}_SHA256SUMS
RUN sha256sum -c terraform_${TERRAFORM_VERSION}_SHA256SUMS
RUN unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip -d /bin
RUN rm -f terraform_${TERRAFORM_VERSION}_linux_amd64.zip
RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh
