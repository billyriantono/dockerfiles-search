ARG VERSION=latest

FROM python:$VERSION

# add os packages and docker cli
RUN apt-get update && apt-get install -y python3-dev netcat git curl gosu apt-transport-https ca-certificates build-essential software-properties-common lsb-release \
    && curl -fsSL https://download.docker.com/linux/$(lsb_release -is | tr '[:upper:]' '[:lower:]')/gpg | apt-key add - 2>/dev/null \
    && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/$(lsb_release -is | tr '[:upper:]' '[:lower:]') $(lsb_release -cs) stable" \
    && apt-get update \
    && apt-get install -y docker-ce-cli

# add vaultenv and wait-for
ADD https://github.com/gendall/vaultenv/releases/download/v0.11.0/vaultenv /usr/local/bin/vaultenv
ADD https://raw.githubusercontent.com/gendalldesign/wait-for/master/wait-for /usr/local/bin/wait-for
RUN chmod +x /usr/local/bin/vaultenv /usr/local/bin/wait-for && ln -s /run/secrets/vault_config /etc/vaultenv.conf
ENV VAULTENV_SECRETS_FILE=/run/secrets/vault_secrets

CMD ["python3"]
