FROM node:alpine

# RUN useradd --user-group --create-home --shell /bin/false app

ENV HOME=/home/app
WORKDIR $HOME

RUN apk update && apk add ca-certificates && update-ca-certificates && apk add wget && apk add docker
RUN npm install -g @angular/cli -g yarn && npm cache clean --force

