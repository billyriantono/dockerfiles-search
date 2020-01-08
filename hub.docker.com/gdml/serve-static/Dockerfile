FROM node:10-alpine

ENV PORT 3000

WORKDIR /
RUN npm i --no-save express@4.16.4

ADD serve.js /
ADD healthcheck.js /

ONBUILD ADD dist/ /srv

HEALTHCHECK CMD node /healthcheck.js localhost ${PORT} / 200

CMD node /serve.js
