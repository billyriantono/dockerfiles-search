FROM node:latest

RUN mkdir -p /usr/src/app
WORKDIR /user/src/app


RUN npm install

ADD src /usr/src/app/src
ADD public /usr/src/app/public

RUN npm build

CMD ["npm", "start"]



