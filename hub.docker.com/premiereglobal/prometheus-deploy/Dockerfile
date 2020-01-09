FROM alpine:3.8

ENV TERRAFORM_VERSION=0.11.14
ENV YQ_VERSION=2.4.1
ENV VAULT_VERSION=1.2.2

VOLUME ["/deploy"]

WORKDIR /deploy

RUN apk update
RUN apk add jq python bash ca-certificates git openssl openssh-client zip curl wget gettext

RUN ln -sf /usr/share/zoneinfo/Etc/UTC /etc/localtime
RUN apk -Uuv add groff less python py-pip
RUN pip install awscli
RUN apk --purge -v del py-pip

RUN rm -rf /var/cache/apk/*
RUN rm -rf /var/tmp/*

RUN cd /tmp && \
    wget https://releases.hashicorp.com/vault/${VAULT_VERSION}/vault_${VAULT_VERSION}_linux_amd64.zip && \
    unzip vault_${VAULT_VERSION}_linux_amd64.zip -d /usr/bin && \
    wget https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
    unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip -d /usr/bin && \
    wget -LO /usr/bin/yq https://github.com/mikefarah/yq/releases/download/${YQ_VERSION}/yq_linux_amd64 && \
    chmod +x /usr/bin/yq && \
    rm -rf /tmp/*

ENV SOCKET_DIR /root/.ssh-agent
ENV SSH_AUTH_SOCK ${SOCKET_DIR}/socket
VOLUME ${SOCKET_DIR}

CMD ssh-agent -a ${SSH_AUTH_SOCK} && tail -f /dev/null
