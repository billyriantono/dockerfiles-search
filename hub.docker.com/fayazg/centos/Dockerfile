FROM centos:latest
MAINTAINER fayazg

ENV TERRAFORM_VERSION=0.11.3

RUN yum -y update && \
    yum --nogpg -y install wget git unzip && \
    yum clean all -y && rm -rf /var/cache/yum /tmp/*

RUN curl -o jq -L https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64
RUN chmod +x jq
RUN mv jq /usr/local/bin/

RUN curl -o terraform.zip https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip
RUN unzip terraform.zip
RUN mv terraform /usr/local/bin/
RUN rm -f terraform*
