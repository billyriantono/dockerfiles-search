FROM node:10.15

ARG $ENV

ENV GATSBY_ACTIVE_ENV=$ENV

WORKDIR /usr/src/app

COPY package*.json /usr/src/app/

RUN npm install && \
  npm install -g gatsby-cli 

COPY . /usr/src/app

RUN GATSBY_ACTIVE_ENV=$ENV gatsby build 

CMD [ "gatsby", "serve",  "--host", "0.0.0.0"]


