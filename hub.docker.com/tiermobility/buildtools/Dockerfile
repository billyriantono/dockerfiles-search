FROM alpine:3.9.2

ENV HELMFILE_VERSION="v0.48.0"
ENV HELM_VERSION="v2.13.1"
ENV KUBECTL_VERSION="v1.13.5"
ENV AWS_IAM_AUTH_VERSION="1.11.5/2018-12-06"
ENV TERRAFORM_VERSION="0.11.13"

RUN apk add --update ca-certificates openssl curl jq git bash docker sudo maven

RUN addgroup -g 3434 circleci \
  && adduser -u 3434 -G circleci -s /bin/bash -D circleci \
  && echo 'circleci ALL=NOPASSWD: ALL' >> /etc/sudoers.d/50-circleci

SHELL ["/bin/bash", "-c"]

ADD https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl /usr/local/bin/kubectl
ADD https://github.com/roboll/helmfile/releases/download/${HELMFILE_VERSION}/helmfile_linux_amd64 /usr/local/bin/helmfile 
ADD https://amazon-eks.s3-us-west-2.amazonaws.com/${AWS_IAM_AUTH_VERSION}/bin/linux/amd64/aws-iam-authenticator /usr/local/bin/aws-iam-authenticator

RUN curl -SL https://storage.googleapis.com/kubernetes-helm/helm-${HELM_VERSION}-linux-amd64.tar.gz | tar xz && \
    mv linux-amd64/helm /usr/local/bin/helm && \
    rm -rf linux-amd64

RUN curl -SL https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip -o terraform.zip && \
    unzip terraform.zip && \
    mv terraform /usr/local/bin/terraform && \
    rm -rf terraform.zip

RUN chmod +x /usr/local/bin/kubectl /usr/local/bin/aws-iam-authenticator /usr/local/bin/helm /usr/local/bin/helmfile /usr/local/bin/terraform

RUN mkdir -p ~/.helm/plugins
RUN helm plugin install https://github.com/futuresimple/helm-secrets

# aws-cli
RUN apk -v --update add \
        python \
        python-dev \
        py-pip \
        groff \
        less \
        mailcap && \
        rm /var/cache/apk/*

RUN pip install --upgrade \
        awscli==1.16.140 \
        s3cmd==2.0.1 \
        python-magic 

RUN pip install --upgrade awsebcli==3.15.0

COPY .datadog .datadog
RUN chmod +x .datadog/*
