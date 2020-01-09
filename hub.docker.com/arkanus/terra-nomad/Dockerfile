FROM frolvlad/alpine-glibc:latest
MAINTAINER Marcos Sánchez <arkanus@gmail.com>

ENV NOMAD_DOWNLOAD_URL=https://releases.hashicorp.com/nomad/0.8.6/nomad_0.8.6_linux_amd64.zip\
	TERRAFORM_DOWNLOAD_URL=https://releases.hashicorp.com/terraform/0.10.8/terraform_0.10.8_linux_amd64.zip

RUN apk add --no-cache wget zip jq python make go gcc git musl-dev openssh-client
RUN GOBIN=/usr/local/bin go get github.com/alshabib/tfjson
RUN cd /tmp &&\
	wget $NOMAD_DOWNLOAD_URL &&\
	unzip nomad*.zip &&\
	mv nomad /usr/local/bin/nomad

RUN cd /tmp &&\
	wget $TERRAFORM_DOWNLOAD_URL &&\
	unzip terraform*.zip &&\
	mv terraform /usr/local/bin/terraform
