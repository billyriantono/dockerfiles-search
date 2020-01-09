FROM node as node
COPY . /app
WORKDIR /app
RUN npm install \
  && npm run generate \
  && find /app/dist -type d \
  | xargs -P0 chmod o+rx \
  && find /app/dist -type f \
  | xargs -P0 chmod o+r

FROM php:7.3.8-apache
LABEL maintainer "genzouw <genzouw@gmail.com>"
RUN a2enmod rewrite
COPY --from=node /app/dist/ /var/www/html/
