FROM node:12

COPY *.json /app/

WORKDIR /app

RUN npm install

COPY src /app/src

COPY ormconfig.json.prod /app/ormconfig.json

EXPOSE 3000

ENV NODE_ENV production

ENTRYPOINT [ "npm", "start" ]
