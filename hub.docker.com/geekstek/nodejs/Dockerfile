FROM node:10-alpine

RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh

WORKDIR /home/node/app

RUN git clone http://willieong:s2c5zrMDrYkqNpK28UcE@bitbucket.org/geekstek/gspj01-nodejs.git /home/node/app

RUN chown -R node:node /home/node/app

USER node

RUN npm install

COPY --chown=node:node . .

EXPOSE 9000

CMD [ "node", "app.js" ]