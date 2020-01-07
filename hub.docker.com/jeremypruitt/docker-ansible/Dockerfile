FROM centos:centos7
MAINTAINER Jeremy Pruitt <jpruitt@juniper.net>
RUN yum clean all && \
    yum -y install epel-release && \
    yum -y install PyYAML python-jinja2 python-httplib2 python-keyczar python-paramiko python-setuptools python-devel gcc git curl wget unzip jq python-pip
RUN mkdir /etc/ansible/
RUN echo -e '[local]\nlocalhost' > /etc/ansible/hosts
RUN pip install ansible
RUN pip install shade

# Install Vault (https://vaultproject.io/)
ENV VAULT_VERSION 0.5.2
RUN mkdir -p /tmp/vault && \
    cd /tmp/vault && \
    curl -L -O https://releases.hashicorp.com/vault/${VAULT_VERSION}/vault_${VAULT_VERSION}_linux_amd64.zip > \
      vault_${VAULT_VERSION}_linux_amd64.zip && \
    unzip vault_${VAULT_VERSION}_linux_amd64.zip && \
    mv vault* /usr/local/bin/ && \
    rm -rf /tmp/vault

# Install envconsul
ENV ENVCONSUL_VERSION 0.6.1
RUN wget --version
RUN wget -q --no-check-certificate -O /tmp/envconsul.zip https://releases.hashicorp.com/envconsul/${ENVCONSUL_VERSION}/envconsul_${ENVCONSUL_VERSION}_linux_amd64.zip
RUN unzip -d /tmp /tmp/envconsul.zip
RUN rm /tmp/envconsul.zip
RUN mv /tmp/envconsul /usr/bin
