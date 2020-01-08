FROM node:8.9-alpine

COPY . /www/app

RUN npm install -g cordova ionic


WORKDIR /www/app
RUN npm install

EXPOSE 8100

CMD ["ionic","serve", "--all", "--port", "8100"]
