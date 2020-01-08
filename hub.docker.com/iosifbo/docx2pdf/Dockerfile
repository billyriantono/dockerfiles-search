FROM node:10

RUN apt-get update && \
    apt-get install -y unoconv libreoffice-writer libreoffice-calc

WORKDIR /usr/src/app

COPY package*.json ./
RUN mkdir files
RUN npm install

COPY . .
EXPOSE 8080

CMD [ "node", "index.js" ]
