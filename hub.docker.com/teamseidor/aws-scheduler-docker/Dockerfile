FROM alpine:3.8

# update packages
RUN apk update

# install dependencies
RUN apk add \
  make \
  openssl \
  git \
  python \
  py-pip \
  bash \
  wget \
  unzip

# install awscli
RUN pip install awscli

# purge cache so
RUN rm -rf /var/cache/apk/*

# install terraform
RUN wget \
  https://releases.hashicorp.com/terraform/0.11.10/terraform_0.11.10_linux_amd64.zip
RUN unzip terraform_0.11.10_linux_amd64.zip && mv terraform /usr/bin

# config vars
ARG AWS_ACCESS_KEY_ID
ARG AWS_SECRET_ACCESS_KEY
ARG AWS_DEFAULT_REGION

# set workdir
WORKDIR /code/terraform

# set entrypoint
ENTRYPOINT /opt/start.sh