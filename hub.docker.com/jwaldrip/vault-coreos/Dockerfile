FROM cgswong/vault:latest
MAINTAINER Oded Lazar <oded@senexx.com>

# install curl
RUN apk-install --no-cache curl


ENV VAULT_LOG_LEVEL info
ENV ETCD_ANNOUNCE_PATH vaults-unsealed
ENV ETCD_ANNOUNCE 1

RUN mkdir /vault
ADD vault.hcl run.sh /vault/

ENTRYPOINT [ "/vault/run.sh" ]
