FROM alpine:3.4

MAINTAINER Danis Yogaswara <danis@aniqma.com>

ENV TERRAFORM_VERSION=0.11.14

RUN apk --no-cache add wget ca-certificates bash openssl unzip git

## Install Terraform in local
RUN wget https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
	unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip -d /usr/local/bin && \
	rm -rf /var/cache/apk/*

RUN chmod +x /usr/local/bin/terraform

RUN apk del wget unzip