FROM node:10

ADD . /connection-database

RUN cd ./connection-database
RUN npm install

EXPOSE 3000

CMD ["node", "/connection-database/test.js"]
