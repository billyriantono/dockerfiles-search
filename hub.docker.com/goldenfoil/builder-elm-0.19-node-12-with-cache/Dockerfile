FROM node:12-alpine 

RUN mkdir /home/node/app && mkdir /home/node/app/donor
WORKDIR /home/node/app/donor
ADD . /home/node/app/donor

RUN apk add yarn && yarn global add elm && elm make src/Main.elm

WORKDIR /home/node/app
RUN rm -rf ./donor