ARG VERSION=latest

FROM mysql:$VERSION

# add vaultenv and wait-for
RUN apt-get update && apt-get install -y netcat ca-certificates
ADD https://github.com/gendall/vaultenv/releases/download/v0.11.0/vaultenv /usr/bin/vaultenv
ADD https://raw.githubusercontent.com/gendalldesign/wait-for/master/wait-for /usr/bin/wait-for
RUN chmod +x /usr/bin/vaultenv /usr/bin/wait-for && ln -s /run/secrets/vault_config /etc/vaultenv.conf
ENV MYSQL_RANDOM_ROOT_PASSWORD=yes VAULTENV_SECRETS_FILE=/run/secrets/vault_secrets

COPY mysql.cnf /etc/mysql/conf.d/docker-mysql-custom.cnf

EXPOSE 3306

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["mysqld"]
