FROM node:8

ADD app.js .
ADD couchService.js .
ADD package.json .

RUN yarn

ENTRYPOINT [ "node", "app.js"]
