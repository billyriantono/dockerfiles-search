FROM node:8.9.0-alpine

RUN apk update \
  && apk add yarn \
  && rm -rf /var/cache/apk/* \
  && rm -rf /tmp/*

RUN yarn global add nodemon --prefix /usr/local

CMD [ "node" ]
