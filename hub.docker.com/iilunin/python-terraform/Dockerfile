FROM python:2.7.13-slim

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ENV TERRAFORM_VERSION=0.9.6
# setup pyton and other prerequisities
RUN \
  apt-get update && \
  apt-get install -y \
    zip \
    unzip \
    curl

# Setup terraform
RUN \
  curl https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip > terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
  unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip -d /bin && \
  rm -f terraform_${TERRAFORM_VERSION}_linux_amd64.zip

VOLUME ["/usr/src/app/"]

CMD bash
