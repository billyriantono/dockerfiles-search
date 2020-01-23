FROM node:8.14-alpine
RUN apk add --update git -y && npm i --global @adonisjs/cli 
WORKDIR /app
EXPOSE 3333
ENTRYPOINT ["adonis"]