FROM alpine:3.6
MAINTAINER "VEBER Arnaud <https://github.com/VEBERArnaud>"

# install bash, ca-certificates & make
RUN apk --update add bash ca-certificates make

# terraform version to install
ENV TERRAFORM_VERSION=0.9.11

# download terraform zip
ADD https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip ./

# install terraform
RUN unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip -d /bin
RUN rm -f terraform_${TERRAFORM_VERSION}_linux_amd64.zip
