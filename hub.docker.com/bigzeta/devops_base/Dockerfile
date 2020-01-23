FROM circleci/python:3.6.1

ARG PACKER_VERSION=1.2.1
ARG TERRAFORM_VERSION=0.11.4
ARG TERRAGRUNT_VERSION=v0.14.2
ARG BINARY_TYPE=linux_amd64
ARG DEBIAN_FRONTEND=noninteractive

ARG H=/home/circleci

# https://releases.hashicorp.com/terraform/0.11.4/terraform_0.11.4_${BINARY_TYPE}.zip
RUN echo "alias ll='ls -alh'" >> ${H}/.bashrc && echo "set -Oq vi" >> ${H}/.bashrc

# Get packer checksum

# Install packer
#
RUN \
wget -q -O /tmp/sha256sums \
"https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_SHA256SUMS"; \
grep ${BINARY_TYPE} /tmp/sha256sums; \
export PACKER_CHECKSUM=$(grep ${BINARY_TYPE} /tmp/sha256sums | cut -d ' ' -f 1); \
export ANOTHER_VAR="this is a test"; \
wget -q -O /tmp/packer.zip \
"https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_${BINARY_TYPE}.zip"; \
echo "${PACKER_CHECKSUM} /tmp/packer.zip" | sha256sum --check - ; \
sudo unzip -oud "/usr/local/bin" /tmp/packer.zip; \
rm /tmp/packer.zip; \
rm /tmp/sha256sums;

# Install terraform
RUN echo "Installing Terraform"; \
wget -q -O /tmp/sha256sums \
"https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_SHA256SUMS"; \
export TERRAFORM_CHECKSUM=$(grep ${BINARY_TYPE} /tmp/sha256sums | cut -d ' ' -f 1); \
wget -q -O /tmp/terraform.zip \
"https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_${BINARY_TYPE}.zip"; \
echo "Downloaded checksum ${TERRAFORM_CHECKSUM}"; \
echo "${TERRAFORM_CHECKSUM} /tmp/terraform.zip" | sha256sum --check - ; \
sudo unzip -oud "/usr/local/bin" /tmp/terraform.zip; \
rm /tmp/terraform.zip;\
rm /tmp/sha256sums

ARG TERRAGRUNT_URL=https://github.com/gruntwork-io/terragrunt/releases/download/v0.13.7/terragrunt_${BINARY_TYPE}

# Install Terragrunt
RUN sudo wget -q -O "/usr/local/bin/terragrunt" \
"https://github.com/gruntwork-io/terragrunt/releases/download/${TERRAGRUNT_VERSION}/terragrunt_${BINARY_TYPE}" ; \
sudo chmod +x /usr/local/bin/terragrunt

# Install jq
RUN sudo wget -q -O "/usr/local/bin/jq" "https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64"; \
sudo chmod +x /usr/local/bin/jq

RUN sudo pip install ansible awscli

# Install nodejs 8.x and npm and yarn, needed to compile assets
RUN curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
RUN sudo apt-get install -y nodejs
RUN sudo npm install -g yarn@latest yuglify@latest

RUN sudo apt-get install rsync

RUN sudo /bin/bash -c 'sudo curl -L https://github.com/docker/compose/releases/download/1.19.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose'
RUN sudo chmod +x /usr/local/bin/docker-compose

RUN curl -sL https://sentry.io/get-cli/ | bash

ADD build_container.bashrc /home/circleci/.bashrc
ARG DEBIAN_FRONTEND=teletype
