FROM node:latest

LABEL maintainer="Duy Hieu"

ENV NODE_ENV=production

ENV PORT=3000
RUN mkdir /var/www

COPY ExpressDocker /var/www
WORKDIR /var/www/

VOLUME ('/home/duyhieu')

RUN npm install

EXPOSE 3000
ENTRYPOINT [ "npm", "start" ]