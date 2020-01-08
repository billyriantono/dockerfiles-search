ARG VERSION=latest

FROM node:$VERSION

ADD https://github.com/gendall/vaultenv/releases/download/v0.11.0/vaultenv /usr/local/bin/vaultenv
RUN chmod +x /usr/local/bin/vaultenv && ln -s /run/secrets/vault_config /etc/vaultenv.conf
ENV NODE_ENV=development VAULTENV_SECRETS_FILE=/run/secrets/vault_secrets

WORKDIR /usr/src/app

EXPOSE 3000 9229

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["node"]
