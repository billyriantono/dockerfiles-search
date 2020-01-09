FROM node:8.12.0-alpine

LABEL maintainer="Picter <developers@picter.com>"

ENV TERRAFORM_VERSION=0.11.7

# Needed linux tools
RUN apk --no-cache add \
	python3 \
	py-crcmod \
	curl \
	bash \
	libc6-compat \
	openssh-client \
	git \
	sudo \
	zip \
	unzip \
	jq

RUN pip3 install awscli

RUN wget https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip &&\
	unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip &&\
	rm terraform_${TERRAFORM_VERSION}_linux_amd64.zip &&\
	sudo mv terraform /usr/local/bin/ &&\
	terraform --version