FROM node:10-alpine

WORKDIR /app

COPY ./ /app

RUN cd /app && \
npm install

CMD ["node", "/app/cmd.js"]