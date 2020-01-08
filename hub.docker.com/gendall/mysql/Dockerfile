ARG VERSION=latest

FROM mysql:$VERSION

ADD https://github.com/gendall/vaultenv/releases/download/v0.11.0/vaultenv /usr/local/bin/vaultenv
RUN chmod +x /usr/local/bin/vaultenv && ln -s /run/secrets/vault_config /etc/vaultenv.conf
ENV VAULTENV_SECRETS_FILE=/run/secrets/vault_secrets

COPY mysql.cnf /etc/mysql/conf.d/docker-mysql-custom.cnf

EXPOSE 3306

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["mysqld"]
