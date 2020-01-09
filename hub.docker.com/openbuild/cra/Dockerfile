FROM node:alpine

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

RUN yarn global add create-react-app --prefix /usr/local
RUN create-react-app /usr/src/app
RUN yarn add --exact react-scripts@2.1.3
RUN yarn cache clean

CMD [ "yarn", "start" ]

EXPOSE 3000
