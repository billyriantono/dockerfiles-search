FROM node:10-alpine

ENV DISCOURSE_BASE_URL ''
ENV DISCOURSE_API_KEY ''
ENV DISCOURSE_USER ''
ENV DISCOURSE_CUSTOM_FIELD_NAME ''
ENV DISCOURSE_USER_LIST_QUERY_ID ''
ENV DISCOURSE_WEBHOOK_SECRET ''
ENV TEAMSPEAK_USERNAME 'serveradmin'
ENV TEAMSPEAK_PASSWORD ''
ENV TEAMSPEAK_HOST 'localhost'
ENV TEAMSPEAK_SERVER_PORT '9987'
ENV TEAMSPEAK_QUERY_PORT '10011'
ENV TEAMSPEAK_PROTOCOL 'raw'
ENV TEAMSPEAK_BOT_NAME 'Bot'
ENV API_KEY ''

RUN mkdir -p /home/node/app/node_modules

RUN mkdir -p /home/node/app/db

RUN mkdir -p /home/node/app/logs

RUN chown -Rh node:node /home/node/app

WORKDIR /home/node/app

COPY package*.json ./

USER node

RUN npm install

COPY --chown=node:node . .

RUN npm run build

EXPOSE 3000

CMD [ "node", "dist/index.js" ]

VOLUME ["/home/node/app/logs", "/home/node/app/db"]