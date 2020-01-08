FROM node:10

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY index.html index.js ./

EXPOSE 8080

CMD [ "node", "index.js" ]
