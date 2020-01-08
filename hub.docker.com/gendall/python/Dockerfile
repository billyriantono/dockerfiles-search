ARG VERSION=latest

FROM python:$VERSION

# add vaultenv and wait-for
RUN apt-get update && apt-get install -y netcat
ADD https://github.com/gendall/vaultenv/releases/download/v0.11.0/vaultenv /usr/local/bin/vaultenv
ADD https://raw.githubusercontent.com/gendalldesign/wait-for/master/wait-for /usr/local/bin/wait-for
RUN chmod +x /usr/local/bin/vaultenv /usr/local/bin/wait-for && ln -s /run/secrets/vault_config /etc/vaultenv.conf
ENV VAULTENV_SECRETS_FILE=/run/secrets/vault_secrets

CMD ["python3"]
