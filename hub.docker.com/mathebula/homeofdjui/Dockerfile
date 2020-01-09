FROM mathebula/nginx-node

MAINTAINER African Developer (mathebula@africandeveloper.co.za)

RUN rm /etc/nginx/conf.d/default.conf
COPY infrastructure/nginx/default.conf /etc/nginx/conf.d/default.conf
COPY infrastructure/nginx/default /etc/nginx/sites-enabled/default

RUN mkdir -p /var/www/
WORKDIR /var/www/
USER root

ENV PATH /var/www/node_modules/.bin:$PATH
COPY package.json /var/www/package.json

RUN npm install --silent

COPY . /var/www/
RUN npm run build
RUN rm -rf src
RUN rm -rf public
RUN rm -rf package.json
RUN rm -rf package-lock.json

CMD ["nginx", "-g", "daemon off;"]
