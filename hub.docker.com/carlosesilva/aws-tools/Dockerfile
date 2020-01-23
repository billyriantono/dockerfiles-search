FROM alpine:3.8

ENV PAGER="less -r"
ENV TERRAFORM_VERSION=0.11.13

# Install required packages
RUN set -ex; \
    apk --no-cache add \
      bash \
      less \
      curl \
      zip \
      git \
      jq \
      groff \
      py-pip \
      python \
      nodejs \
      npm; \
    npm install -g npm;

# Install aws-shell (which also install aws-cli)
RUN pip install --upgrade \
      pip \
      aws-shell \
      awsebcli; \
    echo "complete -C '/usr/bin/aws_completer' aws" >> ~/.bashrc;

# Install Terraform
RUN set -ex; \
    curl -o terraform.zip https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip; \
    unzip terraform.zip -d /usr/bin; \
    rm terraform.zip; \
    echo "complete -C '/usr/bin/terraform' terraform" >> ~/.bashrc;

RUN mkdir /code
WORKDIR /code

CMD [ "aws-shell" ]