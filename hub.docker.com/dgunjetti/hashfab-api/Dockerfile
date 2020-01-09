FROM node:8

WORKDIR /usr/src/app

COPY api/package*.json ./

RUN npm install

COPY api/ .

EXPOSE 3001

CMD [ "node", "index.js" ]
