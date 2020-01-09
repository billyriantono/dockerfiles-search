FROM node:latest
EXPOSE 3000

ADD . /app
WORKDIR /app

RUN npm install
ENTRYPOINT ["node", "app.js"]
