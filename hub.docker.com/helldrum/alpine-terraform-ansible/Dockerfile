FROM alpine:latest

RUN apk --update add python py-pip openssl ca-certificates openssh git && \
  apk --update add --virtual build-dependencies \
  python-dev libffi-dev openssl-dev build-base  && \
  pip install --upgrade pip cffi && \
  pip install ansible virtualenv ansible-lint

ADD https://releases.hashicorp.com/terraform/0.9.2/terraform_0.9.2_linux_amd64.zip .
RUN unzip terraform_0.9.2_linux_amd64.zip && \ 
  chmod +x terraform && \
  mv terraform /usr/bin/terraform

ADD https://github.com/adammck/terraform-inventory/releases/download/v0.7-pre/terraform-inventory_v0.7-pre_linux_amd64.zip .
RUN unzip terraform-inventory_v0.7-pre_linux_amd64.zip && \
  chmod +x terraform-inventory && \
  mv terraform-inventory /usr/bin/terraform-inventory

COPY terraform/gcp_instance.tf /root 
