FROM node:lts-alpine

WORKDIR /opt/app

ENV HOME /opt/app

RUN chmod 777 .

EXPOSE 8080

COPY package.json yarn.lock ./

RUN yarn --prod --no-progress && yarn cache clean

COPY . .

RUN yarn build

USER node

CMD ls -l; ls -l build; env; whoami; yarn start
