FROM alpine:3.10

RUN apk update \
 && apk add --no-cache wget openssh git bash tar gzip ca-certificates curl \
 && rm -rf /var/cache/apk/*

RUN wget --quiet https://releases.hashicorp.com/terraform/0.12.18/terraform_0.12.18_linux_amd64.zip \
  && unzip terraform_0.12.18_linux_amd64.zip \
  && mv terraform /usr/bin \
  && rm terraform_0.12.18_linux_amd64.zip
