FROM alpine:latest
RUN apk update
RUN apk fix
RUN apk add nodejs
RUN apk add nodejs-npm
RUN npm install -g yarn && npm upgrade -g yarn
RUN yarn global add @angular/cli
RUN ng set --global packageManager=yarn

EXPOSE 4200