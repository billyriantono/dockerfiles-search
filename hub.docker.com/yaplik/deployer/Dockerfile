FROM alpine:latest

ENV CONSUL_VERSION 1.5.1
ENV VAULT_VERSION 1.1.3
ENV TERRAFORM_VERSION 0.12.1
ENV KUBECTL_VERSION v1.14.3

# Base packages
RUN apk add -U wget unzip git

# Consul
RUN wget -nv -O /tmp/consul.zip https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip \
 && unzip /tmp/consul.zip \
 && mv consul /usr/bin/consul \
 && chmod 755 /usr/bin/consul \
 && rm /tmp/consul.zip

# Vault
RUN wget -nv -O /tmp/vault.zip https://releases.hashicorp.com/vault/${VAULT_VERSION}/vault_${VAULT_VERSION}_linux_amd64.zip \
 && unzip /tmp/vault.zip \
 && mv vault /usr/bin/vault \
 && chmod 755 /usr/bin/vault \
 && rm /tmp/vault.zip

# Nomad
# we build nomad with NOCGO support manually
ADD nomad-nocgo /usr/bin/nomad

# Terraform
RUN wget -nv -O /tmp/terraform.zip https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
 && unzip /tmp/terraform.zip \
 && mv terraform /usr/bin/terraform \
 && chmod 755 /usr/bin/terraform \
 && rm /tmp/terraform.zip

# Kubectl
RUN wget -nv -O /usr/bin/kubectl https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl \
 && chmod 755 /usr/bin/kubectl

# Git FTP
ADD git-ftp /usr/bin/git-ftp
RUN chmod 0755 /usr/bin/git-ftp
