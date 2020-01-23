ARG VERSION=latest

FROM mongo:$VERSION

# add vaultenv and wait-for
RUN apt-get update && apt-get install -y netcat
ADD https://github.com/gendall/vaultenv/releases/download/v0.11.0/vaultenv /usr/bin/vaultenv
ADD https://raw.githubusercontent.com/gendalldesign/wait-for/master/wait-for /usr/bin/wait-for
RUN chmod +x /usr/bin/vaultenv /usr/bin/wait-for && ln -s /run/secrets/vault_config /etc/vaultenv.conf
ENV VAULTENV_SECRETS_FILE=/run/secrets/vault_secrets

EXPOSE 27017

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["mongod"]
