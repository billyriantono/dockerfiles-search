FROM node:8-alpine

# Instala pacotes
RUN apk update && apk add --update --no-cache \ 
    git \
    bash \
    curl \ 
    openssh \
    py-pip

# Atualiza NPM
RUN npm config set unsafe-perm true
RUN npm update -g

# Instala AWSCLI
RUN pip install --upgrade pip && \
    pip install --upgrade awscli

# Instala Serverless Framework
RUN yarn global add serverless

# Cria diretorio para a aplicacao
RUN mkdir /app
WORKDIR /app