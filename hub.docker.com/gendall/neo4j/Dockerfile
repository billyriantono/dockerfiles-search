ARG VERSION=latest

FROM neo4j:$VERSION

# add vaultenv and wait-for
RUN apt-get update && apt-get install -y netcat
ADD https://github.com/gendall/vaultenv/releases/download/v0.11.0/vaultenv /usr/bin/vaultenv
ADD https://raw.githubusercontent.com/gendalldesign/wait-for/master/wait-for /usr/bin/wait-for
RUN chown 999:999 /usr/bin/wait-for && chmod +x /usr/bin/vaultenv /usr/bin/wait-for && \
  ln -s /run/secrets/vault_config /etc/vaultenv.conf
ENV VAULTENV_SECRETS_FILE=/run/secrets/vault_secrets

COPY entrypoint.sh /usr/bin/docker-entrypoint.sh
RUN chown 999:999 /usr/bin/docker-entrypoint.sh

# change uid/gid to match the one used with the standard debian install
# this makes permissions easier when mounting volumes across containers
USER 999:999

EXPOSE 7474 7473 7687

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["neo4j"]
