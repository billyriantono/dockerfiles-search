FROM ubuntu:latest
MAINTAINER Keunhak Lim<limkeunhak@gamil.com>

RUN apt-get update
RUN apt-get install -y nodejs npm

ADD assets /var/www/assets
ADD middleware /var/www/middleware
ADD plugins /var/www/plugins
ADD static /var/www/static
ADD components /var/www/components
ADD layouts /var/www/layouts
ADD pages /var/www/pages
ADD store /var/www/store
ADD nuxt.config.js /var/www/nuxt.config.js
ADD package.json /var/www/package.json

WORKDIR /var/www
RUN npm install

# Webpack issue: https://github.com/webpack/webpack/issues/8768
RUN npm uninstall ajv
RUN npm install ajv@6.8.1

CMD npm run dev

EXPOSE 3000
