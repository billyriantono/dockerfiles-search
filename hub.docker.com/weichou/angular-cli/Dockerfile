FROM node:7.5

ENV HOME=/usr/src/app
RUN mkdir $HOME
WORKDIR $HOME

RUN npm install -g @angular/cli && npm cache clean

EXPOSE 4200
EXPOSE 49153