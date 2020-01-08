# Nuxt
FROM mobydigital/node-template

LABEL authors="Yoelnacho"

RUN npm i npm@latest -g \
    && npm i -g npx \
    && npm cache verify

# Copies all the content
COPY . /usr/app