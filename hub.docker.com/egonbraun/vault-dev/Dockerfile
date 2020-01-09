FROM ubuntu:16.04
MAINTAINER Egon Braun @egonbraun

ENV VAULT_VERSION 0.6.2
ENV VAULT_ARCH amd64
ENV INSTALL_DIR /opt/vault

WORKDIR ${INSTALL_DIR}

COPY ./vault.hcl ${INSTALL_DIR}/vault.hcl

RUN apt-get update && \
    apt-get install unzip wget -y && \
    wget -q "https://releases.hashicorp.com/vault/${VAULT_VERSION}/vault_${VAULT_VERSION}_linux_${VAULT_ARCH}.zip" && \
    unzip "vault_${VAULT_VERSION}_linux_${VAULT_ARCH}.zip" && \
    rm -f "vault_${VAULT_VERSION}_linux_${VAULT_ARCH}.zip" && \
    chmod 755 "${INSTALL_DIR}/vault" && \
    ln -s "${INSTALL_DIR}/vault" "/usr/local/bin" && \
    ln -s "${INSTALL_DIR}/vault.hcl" "/etc" && \
    apt-get autoclean && \
    apt-get --purge -y autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 8201

ENTRYPOINT [                  \
  "/usr/local/bin/vault",     \
  "server",                   \
  "-dev",                     \
  "-config", "/etc/vault.hcl" \
]
