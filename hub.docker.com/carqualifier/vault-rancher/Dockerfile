FROM cgswong/vault:latest

ENV VAULT_ADDR http://0.0.0.0:8200

ADD entry.sh /entry.sh

ENTRYPOINT ["/entry.sh"]
