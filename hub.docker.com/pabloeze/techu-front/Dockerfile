FROM node:8.16.1-jessie

RUN mkdir -p /app/dist && \
    chown -R node:node /app

WORKDIR /app

COPY server/server.js ./
COPY server/package*.json ./
COPY dist/* ./dist/

USER node

RUN npm install

COPY --chown=node:node . .

EXPOSE 8080

CMD [ "node", "server.js" ]