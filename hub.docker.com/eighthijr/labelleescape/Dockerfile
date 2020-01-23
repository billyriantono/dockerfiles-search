FROM node:8

ADD ./client /var/www/client
ADD ./server /var/www/server
ADD ./test /var/www/test
ADD ./config /var/www/config
ADD ./scripts /var/www/scripts
ADD ./package.json /var/www/package.json
ADD ./.babelrc /var/www/.babelrc

WORKDIR /var/www

RUN npm install
RUN npm run build


CMD ["npm", "start"]