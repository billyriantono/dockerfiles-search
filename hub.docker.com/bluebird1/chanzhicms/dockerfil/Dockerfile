FROM node:alpine

WORKDIR /usr/src/app

ADD package.json package-lock.json tsconfig.json /usr/src/app/

RUN npm install

RUN npm install -g typescript

ADD src /usr/src/app/src

RUN tsc

CMD ["node","dist/app.js"]