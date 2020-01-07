FROM node:12

COPY *.json /app/

WORKDIR /app

RUN npm install

COPY index.js /app/

EXPOSE 8080

ENV NODE_ENV production

CMD [ "npm", "start" ]
