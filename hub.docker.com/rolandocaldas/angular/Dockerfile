FROM node:10.11.0-alpine

RUN npm install -g typescript @angular/cli ionic

WORKDIR "/application"

EXPOSE 8080

CMD [ "npm", "run", "server" ]
