# Vue CLI
FROM mobydigital/node-template

LABEL authors="Yoelnacho"

RUN npm i npm@latest -g \
    && npm i -g @vue/cli \
    && npm cache verify

# Copies all the content
COPY . /usr/app/

# User
USER node