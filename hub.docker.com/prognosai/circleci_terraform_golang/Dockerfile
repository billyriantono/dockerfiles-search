FROM circleci/golang:1.10
ENV PS1='🐳 > '

USER root

RUN curl https://releases.hashicorp.com/terraform/0.11.11/terraform_0.11.11_linux_amd64.zip -o terraform_0.11.11_linux_amd64.zip \
  && unzip terraform_0.11.11_linux_amd64.zip \
  && mv terraform /usr/bin \
  && rm terraform_0.11.11_linux_amd64.zip

USER circleci