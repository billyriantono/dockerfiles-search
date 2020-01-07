FROM ubuntu:18.04

ENV AWS_CLI_VERSION 1.16.210

# Helm 2.11.0
ADD https://storage.googleapis.com/kubernetes-helm/helm-v2.11.0-linux-amd64.tar.gz helm-linux-amd64.tar.gz
RUN tar -zxvf helm-linux-amd64.tar.gz && \
    mv linux-amd64/helm /usr/local/bin/helm

# Kubectl for AWS EKS
ADD https://amazon-eks.s3-us-west-2.amazonaws.com/1.13.7/2019-06-11/bin/linux/amd64/kubectl /usr/local/bin/kubectl
RUN chmod +x /usr/local/bin/kubectl

# AWS IAM Authenticator.
ADD https://amazon-eks.s3-us-west-2.amazonaws.com/1.13.7/2019-06-11/bin/linux/amd64/aws-iam-authenticator /usr/local/bin/aws-iam-authenticator
RUN chmod +x /usr/local/bin/aws-iam-authenticator

# Python 2.7 with pip
RUN apt-get update && apt-get install -y \
        python-pip \
        unzip \
        git \
        curl

# AWS CLI
RUN pip install awscli==${AWS_CLI_VERSION}

# Terraform
ADD https://releases.hashicorp.com/terraform/0.12.10/terraform_0.12.10_linux_amd64.zip terraform.zip
RUN unzip terraform.zip && \
    mv ./terraform /usr/local/bin && \
    chmod +x /usr/local/bin/terraform

CMD []

WORKDIR /data
