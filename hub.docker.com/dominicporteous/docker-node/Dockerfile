FROM alpine:3.1
RUN apk add --update nodejs git

ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 5.1.0
ENV NPM_ENV production
ENV NODE_ENV production

WORKDIR /var/www

RUN sh -c 'if [ -f "/var/www/package.json" ]; then npm i --production ; fi'
RUN sh -c "if [ -f "/var/www/package.json" ]; then touch err.log && touch out.log && echo '\!{.git}/**}' | tee .foreverignore; fi"

#Expose the port
EXPOSE 8080
#CMD npm start
