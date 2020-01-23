# build assets in a node image

FROM node:8 as builder

ENV NODE_ENV=development

WORKDIR /app

RUN yarn global add gulp

COPY package.json gulpfile.js ./

RUN yarn install

COPY plugins plugins

COPY themes themes

RUN yarn build


# spin up a wordpress image and copy only the built things

FROM wordpress:4.9-php7.0-apache

WORKDIR /var/www/html

COPY --from=builder --chown=www-data:www-data /app/plugins wp-content/plugins

COPY --from=builder --chown=www-data:www-data /app/themes wp-content/themes
