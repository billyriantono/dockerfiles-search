FROM node:alpine

ENV TEAMSPEAK_USERNAME 'serveradmin'
ENV TEAMSPEAK_PASSWORD ''
ENV TEAMSPEAK_HOST 'localhost'
ENV TEAMSPEAK_SERVER_PORT '9987'
ENV TEAMSPEAK_QUERY_PORT '10011'
ENV TEAMSPEAK_PROTOCOL 'raw'
ENV WEBHOOK_URL ''
ENV DEBUG ''

RUN mkdir -p /home/node/app/node_modules

RUN mkdir -p /home/node/app/logs

RUN chown -Rh node:node /home/node/app

WORKDIR /home/node/app

COPY package*.json ./

USER node

RUN npm install

COPY --chown=node:node . .

EXPOSE 3000

CMD [ "npm", "start" ]

VOLUME ["/home/node/app/logs"]