FROM node:8-alpine

# Instala pacotes
RUN apk update && apk add --update --no-cache \ 
    git \
    bash \
    curl \ 
    openssh \
    py-pip \
    zip

# Atualiza NPM
RUN npm config set unsafe-perm true
RUN npm update -g

# npm install dotenv
RUN npm install dotenv -g

# Instala o newman
RUN npm install -g newman
RUN npm install newman-reporter-html

# Instala o Knex
RUN npm install knex mysql -g

# Instala AWSCLI
RUN pip install --upgrade pip && \
    pip install --upgrade awscli