FROM node:10-alpine
WORKDIR /home/node/app
COPY package*.json ./
RUN npm install
COPY . .
RUN mkdir -p /home/node/.config/toogoodtogo-watcher-nodejs && \
    chown -R node:node /home/node/.config
USER node
VOLUME /home/node/.config/toogoodtogo-watcher-nodejs
CMD [ "node", "index.js", "watch" ]
