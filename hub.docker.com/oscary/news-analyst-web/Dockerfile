FROM node:12

WORKDIR /usr/src/app

COPY ./ ./

RUN yarn
RUN yarn build

EXPOSE 3000

ENTRYPOINT yarn start
