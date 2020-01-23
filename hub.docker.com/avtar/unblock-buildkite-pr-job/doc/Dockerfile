FROM node:12.6.0

EXPOSE 8080

ENV wd ./src

ADD ./src $wd

WORKDIR ${wd}

RUN npm install

CMD ["node", "index.js"]