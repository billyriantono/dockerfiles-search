ARG VERSION=latest

FROM neo4j:$VERSION

ADD https://github.com/gendall/vaultenv/releases/download/v0.11.0/vaultenv /usr/local/bin/vaultenv
RUN chmod +x /usr/local/bin/vaultenv && ln -s /run/secrets/vault_config /etc/vaultenv.conf
ENV VAULTENV_SECRETS_FILE=/run/secrets/vault_secrets

EXPOSE 7474 7473 7687

ENTRYPOINT ["/sbin/tini", "-g", "--", "/docker-entrypoint.sh"]
CMD ["neo4j"]
