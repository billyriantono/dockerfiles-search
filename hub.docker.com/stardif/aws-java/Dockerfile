FROM maven:3-jdk-8

RUN apt-get update                             && \
    apt-get install -qqy groff-base python-pip && \
    apt-get clean                              && \
    pip install awscli                         && \
    wget -O terraform.zip 'https://releases.hashicorp.com/terraform/0.11.11/terraform_0.11.11_linux_amd64.zip' && \
    unzip -d /usr/bin terraform.zip
