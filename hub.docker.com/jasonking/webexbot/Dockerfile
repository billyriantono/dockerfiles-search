FROM node:12-alpine

COPY . /app

RUN cd /app \
  && npm install --production

WORKDIR /app

CMD ["node", "bot.js"]
