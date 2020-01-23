FROM ubuntu:18.04 as build

RUN set -eux \
	&& apt-get update -qq \
	&& apt-get install -qq -y --no-install-recommends --no-install-suggests \
		ca-certificates \
		curl \
		git \
		unzip

ARG TG_VERSION=v0.21.8
ARG TF_VERSION=0.12.17

# Get Terraform
RUN curl -sS -L -O https://releases.hashicorp.com/terraform/${TF_VERSION}/terraform_${TF_VERSION}_linux_amd64.zip \
	&& unzip terraform_${TF_VERSION}_linux_amd64.zip \
	&& mv terraform /usr/bin/terraform \
	&& chmod +x /usr/bin/terraform

# Get Terragrunt
RUN set -eux \
	&& curl -sS -L \
		https://github.com/gruntwork-io/terragrunt/releases/download/${TG_VERSION}/terragrunt_linux_amd64 \
		-o /usr/bin/terragrunt \
	&& chmod +x /usr/bin/terragrunt

WORKDIR /config

CMD ["terragrunt", "--version"]
