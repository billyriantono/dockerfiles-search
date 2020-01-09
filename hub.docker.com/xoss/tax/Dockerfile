FROM quay.io/amadeusmuc/base:node-8

COPY . /usr/src/app

RUN npm install --silent;
RUN npm run test-unit

EXPOSE 80

CMD [ "npm", "start" ]
