FROM node:8.10.0

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY . /usr/src/app
RUN yarn

EXPOSE 3000
CMD [ "yarn", "start" ]

