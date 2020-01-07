FROM node:8-alpine

# Instala pacotes
RUN apk update && apk add --update --no-cache \
    git \
    bash \
    curl \
    openssh \
    py-pip \
    py-cryptography \
    wget \
    curl

RUN apk --no-cache add --virtual builds-deps build-base python

# Atualiza NPM
RUN npm config set unsafe-perm true
RUN npm update -g

# Instala AWSCLI
RUN pip install --upgrade pip && \
    pip install --upgrade awscli

# Instala Serverless Framework
RUN npm install -g serverless@1.41.1
RUN npm install serverless-encrypt-enviroment-variables@2.0.0
RUN npm install serverless-domain-manager
RUN npm install serverless-plugin-existing-s3

# Copia scripts
RUN mkdir /scripts
COPY ./scripts /scripts
RUN chmod +x -R /scripts/*.sh

# Cria diretorio para a aplicação
RUN mkdir /app
WORKDIR /app

CMD [ "/bin/sh", "/scripts/deploy.sh" ]