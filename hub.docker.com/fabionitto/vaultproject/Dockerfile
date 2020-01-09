FROM centos:6.7
MAINTAINER Fabio Nitto "fabio.nitto@gmail.com"

RUN yum update -y \
  && yum install -y wget unzip \ 
  && wget https://releases.hashicorp.com/vault/0.5.2/vault_0.5.2_linux_amd64.zip \
  && unzip vault_0.5.2_linux_amd64.zip \
  && mv vault /usr/local/bin/ \
  && rm -f vault_0.5.2_linux_amd64.zip

RUN groupadd -r vault \
  && useradd -r -g vault vault \
  && mkdir /vault

COPY vault.hcl /vault/vault.hcl
#COPY entrypoint.sh /usr/local/bin/
COPY start.sh /usr/local/bin/

EXPOSE 8200
#ENTRYPOINT [ "entrypoint.sh" ]

CMD [ "start.sh" ]
